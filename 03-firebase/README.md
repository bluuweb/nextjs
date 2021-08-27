# Firebase Auth

- [Example nextjs firebase](https://github.com/vercel/next.js/tree/canary/examples/with-firebase)
- [Github: Branch 01-context-api](https://github.com/bluuweb/nextjs-firebase/tree/01-provider)
- [Github: Branch 02-auth-google](https://github.com/bluuweb/nextjs-firebase/tree/02-auth-google)
- []()
- []()

## Instalación

```
npm i firebase
npm i bootstrap // opcional
```

## firebase/clientApp.js
```js
import firebase from "firebase/app";
import "firebase/auth";

const clientCredentials = {
    apiKey: process.env.NEXT_PUBLIC_FIREBASE_API_KEY,
    authDomain: process.env.NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN,
    projectId: process.env.NEXT_PUBLIC_FIREBASE_PROJECT_ID,
    storageBucket: process.env.NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET,
    messagingSenderId: process.env.NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID,
    appId: process.env.NEXT_PUBLIC_FIREBASE_APP_ID,
};

if (!firebase.apps.length) {
    firebase.initializeApp(clientCredentials);
}

export default firebase;
```

## context/userContext.js
```js
import { useRouter } from "next/router";
import { useState, useEffect, createContext, useContext } from "react";
import firebase from "../firebase/clientApp";

export const UserContext = createContext();

export default function UserContextComp({ children }) {
    const router = useRouter();

    const [user, setUser] = useState(null);
    const [loadingUser, setLoadingUser] = useState(true);

    useEffect(() => {
        const unsubscriber = firebase.auth().onAuthStateChanged((user) => {
            try {
                if (user) {
                    const { uid, displayName, email, photoURL } = user;
                    setUser({ uid, displayName, email, photoURL });
                } else setUser(null);
            } catch (error) {
                console.log(error);
            } finally {
                setLoadingUser(false);
            }
        });

        return () => unsubscriber();
    }, []);

    const loginGoogle = async () => {
        try {
            const provider = new firebase.auth.GoogleAuthProvider();
            await firebase.auth().signInWithPopup(provider);
            router.push("/perfil");
        } catch (error) {
            console.log(error);
        }
    };

    const cerrarSesion = () => firebase.auth().signOut();

    return (
        <UserContext.Provider
            value={{ user, setUser, loadingUser, cerrarSesion, loginGoogle }}
        >
            {children}
        </UserContext.Provider>
    );
}

export const useUser = () => useContext(UserContext);
```

## pages/_app.js
```js
import UserProvider from "../context/userContext";
import "bootstrap/dist/css/bootstrap.min.css";

function MyApp({ Component, pageProps }) {
    return (
        <UserProvider>
            <Component {...pageProps} />
        </UserProvider>
    );
}

export default MyApp;
```

## pages/index.jsx
```jsx
import Layout from "../components/layout/Layout";
import { useUser } from "../context/userContext";

export default function Home() {
    const { loadingUser } = useUser();

    if (loadingUser) return <div className="container">Cargando</div>;

    return (
        <Layout>
            <h1>Acceso pública</h1>
        </Layout>
    );
}
```

## pages/perfil.jsx
```jsx
import { useRouter } from "next/router";
import { useEffect } from "react";
import { useUser } from "../context/userContext";

import Layout from "../components/layout/Layout";

const Perfil = () => {
    const { loadingUser, user } = useUser();
    const router = useRouter();

    useEffect(() => {
        if (!loadingUser) {
            if (!user) {
                router.push("/");
            }
        }
    }, [user, loadingUser, router]);

    if (loadingUser || user === null)
        return <div className="container">Cargando</div>;

    return (
        <Layout>
            <h1>Acceso Restringido</h1>
        </Layout>
    );
};

export default Perfil;
```

## components/layout/Layout.jsx
```jsx
import Navbar from "./Navbar";

const Layout = ({ children }) => {
    return (
        <>
            <Navbar />
            <main className="container">{children}</main>
        </>
    );
};

export default Layout;
```

## components/layout/Navbar.jsx

```jsx
import Link from "next/link";
import { useUser } from "../../context/userContext";

const Navbar = () => {
    const { cerrarSesion, user, loginGoogle } = useUser();

    return (
        <nav className="navbar navbar-dark bg-dark">
            <div className="container">
                <Link href="/">
                    <a className="navbar-brand">Firebase</a>
                </Link>
                <div>
                    {user ? (
                        <div className="btn btn-danger" onClick={cerrarSesion}>
                            Salir
                        </div>
                    ) : (
                        <button
                            className="btn btn-primary"
                            onClick={loginGoogle}
                        >
                            Google
                        </button>
                    )}
                </div>
            </div>
        </nav>
    );
};

export default Navbar;
```