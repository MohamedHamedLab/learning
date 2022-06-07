#  UI Frameworks
### Integrating SASS with Next.js

```properties
yarn add sass
```

- Let's look at a simple example. If we open the `pages/index.js`

```jsx
import styles from '../styles/Home.module.scss';
export default function Home() {
  return (
    <div className={styles.homepage}>
      <h1> Welcome to the CSS Modules example </h1>
    </div>
  );
}
```
### Integrating TailwindCSS in Next.js
- TailwindCSS only requires three devDependencies
```properties
yarn add -D autoprefixer postcss tailwindcss
```
-  to manage the dark/light theme

```properties
yarn add next-themes

```
- Now that we have all the dependencies installed

```properties
npx tailwindcss init -p
```
This will create two different files:
1. **tailwind.config.js**: This file will help us configure the TailwindCSS theme, unused CSS purge, dark mode, plugins, and more
2. **postcss.config.js**: TailwindCSS uses PostCSS under the hood and ships with a pre-configured **postcss.config.js** that we can always edit as we prefer.
3. First of all, we want to configure TailwindCSS to remove unused CSS from the final build. 

```json
module.exports = {
  purge: ['./pages/**/*.{js,jsx}', 
    './components/**/*.{js,jsx}'],
  darkMode: 'class',
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```
- We also set the **darkMode** property to **'class'**. That way, the framework will look at the **html** class element to determine whether we need to render the components using dark or  light mode.

```jsx
import { ThemeProvider } from 'next-themes';
import TopBar from '../components/TopBar';
import 'tailwindcss/tailwind.css';
function MyApp({ Component, pageProps }) {
  return (
    // attribute="class" will set a "dark" CSS class
    // to the main <html> tag
    <ThemeProvider attribute="class"> 
      <div
        className="dark:bg-gray-900 bg-gray-50 w-full min-  
           h-screen"
      >
        <TopBar />
        <Component {...pageProps} />
      </div>
    </ThemeProvider>
  );
}
export default MyApp;
```

- to switch theme

```jsx
// ThemeSwitch component
import { useTheme } from 'next-themes';
function ThemeSwitch() {
  const { theme, setTheme } = useTheme();
  const dark = theme === 'dark';
  const toggleTheme = () => {
    setTheme(dark ? 'light' : 'dark');
  };
  if (typeof window === 'undefined') return null;
  return (
    <button
      onClick={toggleTheme}
      className="
        dark:bg-green-900 dark:bg-opacity-20 dark:text-
          gray-50
        bg-green-100 text-gray-500 pl-2 pr-2 rounded-md 
          text-xs
        p-1"
    >
      Toggle theme
    </button>
  );
}
export default ThemeSwitch;
//top nav
import ThemeSwitch from '../ThemeSwitch';
function TopBar() {
  return (
    <div className="w-full p-2 bg-green-500">
      <div className="w-10/12 m-auto">
        <ThemeSwitch />
      </div>
    </div>
  );
}
export default TopBar;
```