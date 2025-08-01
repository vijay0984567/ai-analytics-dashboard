# Airframe React

- [**View Demo**](https://airframe-react-lime.vercel.app)

![aiframe-2019-light-primary-ExchangeTrading2x-bfc026c1-0477-45c8-ba55-f6dd43141e4c](https://user-images.githubusercontent.com/2330394/63061353-20ea4600-bef5-11e9-84c8-000a6dceea4d.png)

# Introduction

**Airframe Dashboard** with a minimalist design and innovative Light UI will let you build an amazing and powerful application with great UI. Perfectly designed for large scale applications, with detailed step by step documentation.

This **Airframe** project is a typical Webpack based React app, also included together with customised [reactstrap](https://reactstrap.github.io). This project has all of it's few dependencies up to date and it will be updated on a regular basis.

# Features

**Airframe Dashboard** has a huge collection of components that can be used in a great number of combinations and variations. It can be used in all types of custom web applications such as **CRMs**, **CMSs**, **Admin Panels**, **Admin Dashboards**, **Analytics**, etc.

- **10+ Layout Variations** - a multitude of possibilities to rearrange the layout, allows to customize the look of your application just as you imagined.
- **Applications** - applications ready, allows you to save time and focus on project development.
- **UI Components** - we offer you a large number of UI components; fully ready for changes that will customize them for your needs.
- **Responsive Design** - fully adapted to your application, exactly well presented on the desktop, a tablet or smartphone.
- **120+ Unique Pages** designed to make use of them directly in your application.
- **2 Starters** so that you can immediately work with the components that are necessary for your application.

# Author

**Vijay Kumar:**

- Github: [https://github.com/vijay0984567](https://github.com/vijay0984567)
- Linkedin: [https://www.linkedin.com/in/vijay0987/](https://www.linkedin.com/in/vijay0987/)
- X: [https://x.com/092Vijaykumar](https://x.com/092Vijaykumar)

# Installation

## Initial Configuration:
You need to have [NodeJs](https://nodejs.org/en/) (>= 10.0.0) installed on your local machine, before attempting to run a dev environment.

1. Extract contents of the package to your local machine.
2. Using the Terminal navigate to the extracted contents.
3. Run `npm install`.

Make sure you have a file called `.npmrc` in the extracted directory. Those files are typically hidden in Unix based systems.

### Development
To start the development environment type `npm start` in the console. This will start a development server with hot reloading enabled.

### Production
To create a production build type `npm run build:prod`. After the process is complete you can copy the output from the `/dist/` directory. The output files are minified and ready to be used in a production environment.

### Build Customization
You can customize the build to suit your specific needs by adjusting the [Webpack](https://webpack.js.org) configuration files. Those files can be found in the `/build` directory. For more details checkout the documentation of WebPack.

## Project Details
Some points of interest about the project project structure:

* `app/components` - custom React components should go here
* `app/styles` - styles added here won't be treated as CSS Modules, so any global classes or library styles should go here
* `app/layout` - the `AppLayout` component can be found here which hosts page contents within itself; additional sidebars and navbars should be placed in `./components/` subdir.
* `app/colors.js` - exports an object with all of the defined colors by the Dashboard. Useful for styling JS based components - for example charts.
* `app/routes` - PageComponents should be defined here, and imported via `index.js`. More details on that later.

### Defining Routes
Route components should be placed in separate directories inside the `/routes/` directory. Next you should open `/routes/index.js` file and attach the component. You can do this in two diffrent ways:

#### Static Imports
Pages imported statically will be loaded eagerly on PageLoad with all of the other content. There will be no additional loads when navigating to such pages **BUT** the initial app load time will also be longer. To add a statically imported page it should be done like this:

```jsx
// Import the default component
import SomePage from './SomePage';
// ...
export const RoutedContent = () => {
    return (
        <Switch>
            { /* ... */ }
            { /* Define the route for a specific path */ }
            <Route path="/some-page" exact component={SomePage} />
            { /* ... */ }
        </Switch>
    );
}
```

#### Dynamic Imports
Dynamically imported pages will only be loaded when they are needed. This will decrease the size of the initial page load and make the App load faster. You can use `React.Suspense` to achieve this. Example:
```jsx
// Create a Lazy Loaded Page Component Import
const SomeAsyncPage = React.lazy(() => import('./SomeAsyncPage'));
// ...
export const RoutedContent = () => {
    return (
        <Switch>
            { /* ... */ }
            { /*
                Define the route and wrap the component in a React.Suspense loader.
                The fallback prop might contain a component which will be displayed
                when the page is loading.
            */ }
            <Route path="/some-async-page">
                <React.Suspense fallback={ <PageLoader /> }>
                    <SomeAsyncPage />
                </React.Suspense>
            </Route>
        </Switch>
    );
}
``` 
#### Route specific Navbars and Sidebars
Sometimes you might want to display additional content in the Navbar or the Sidebar. To do this you should define a customized Navbar/Sidebar component and attach it to a particular route. Example:

```jsx
import { SidebarAlternative } from './../layout/SidebarAlternative';
import { NavbarAlternative } from './../layout/NavbarAlternative';
// ...
export const RoutedNavbars  = () => (
    <Switch>
        { /* Other Navbars: */}
        <Route
            component={ NavbarAlternative }
            path="/some-custom-navbar-route"
        />
        { /* Default Navbar: */}
        <Route
            component={ DefaultNavbar }
        />
    </Switch>  
);

export const RoutedSidebars = () => (
    <Switch>
        { /* Other Sidebars: */}
        <Route
            component={ SidebarAlternative }
            path="/some-custom-sidebar-route"
        />
        { /* Default Sidebar: */}
        <Route
            component={ DefaultSidebar }
        />
    </Switch>
);
```

## Theming
You can set the color scheme for the sidebar and navbar by providing `initialStyle` and `initialColor` to the `<ThemeProvider>` component which should be wrapping the `<Layout>` component.

Possible `initialStyle` values:
* `light`
* `dark`
* `color`

Possible `initialColor` values:
* `primary`
* `success`
* `info`
* `warning`
* `danger`
* `indigo`
* `purple`
* `pink`
* `yellow`

### Programatic Theme Changing
You can change the color scheme on runtime by using the `ThemeConsumer` from the components. Example:
```jsx
// ...
import { ThemeContext } from './../components';
// ...
const ThemeSwitcher = () => (
    <ThemeConsumer>
        ({ onChangeTheme }) => (
            <React.Fragment>
                <Button onClick={() => onThemeChange({ style: 'light' })}>
                    Switch to Light
                </Button>
                <Button onClick={() => onThemeChange({ style: 'dark' })}>
                    Switch to Dark
                </Button>
            </React.Fragment>
        )
    </ThemeConsumer>
);

```

Options provided by the `ThemeConsumer`:
* **style** - current theme style
* **color** - current theme color
* **onChangeTheme({ style?, color? })** - allows to change the theme
