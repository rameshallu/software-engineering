# Next.js Pages Router

The Next.js Pages Router allows you to define routes for your application using the file system. Each file inside the `pages` directory becomes a route in your application. Here's how you can use the Pages Router effectively:

### Basic Routing:

1. **Create Pages:**

   - Inside the `pages` directory, create `.js`, `.jsx`, `.ts`, or `.tsx` files to define your routes.
   - For example, `pages/index.js` defines the route `/`, and `pages/about.js` defines the route `/about`.

2. **Nested Routes:**

   - You can create nested routes by creating subdirectories inside the `pages` directory.
   - For example, `pages/products/index.js` defines the route `/products`, and `pages/products/[id].js` defines dynamic route parameters.

3. **Dynamic Routes:**
   - Use square brackets (`[]`) in the file name to define dynamic routes with parameters.
   - For example, `pages/posts/[id].js` defines a dynamic route with the parameter `id`.

### Linking Between Pages:

1. \*\*`

```jsx
import Link from "next/link";

function MyComponent() {
  return (
    <div>
      {/* Navigate to the /about page */}
      <Link href="/about">
        <a>About</a>
      </Link>
      {/* Navigate to the /products page */}
      <Link href="/products">
        <a>Products</a>
      </Link>
      {/* Navigate to a dynamic route with parameter */}
      <Link href="/posts/[id]" as="/posts/123">
        <a>Post 123</a>
      </Link>
    </div>
  );
}
```

### Accessing Router Information:

1. **`useRouter` Hook:**
   - Use the `useRouter` hook from `next/router` to access information about the current route.
   - You can get query parameters, route parameters, and more using this hook.

```jsx
import { useRouter } from "next/router";

function MyComponent() {
  const router = useRouter();

  // Get query parameters
  const { query } = router;

  // Get route parameters
  const { id } = router.query;

  return (
    <div>
      {/* Display route parameter */}
      <p>Post ID: {id}</p>
    </div>
  );
}
```

### Customizing Routes:

1. **Customizing Route Behavior:**
   - You can customize route behavior using `getStaticProps`, `getStaticPaths`, `getServerSideProps`, and `getInitialProps`.
   - These functions allow you to fetch data at build time, server-side, or client-side and pass it as props to your components.

### Redirects and Rewrites:

1. **Redirects:**

   - Use the `redirects` property in `next.config.js` to define redirects.
   - For example, `{ "source": "/old-page", "destination": "/new-page", "permanent": true }` redirects `/old-page` to `/new-page` permanently.

2. **Rewrites:**
   - Use the `rewrites` property in `next.config.js` to define rewrites.
   - For example, `{ "source": "/blog/:slug", "destination": "/posts/:slug" }` rewrites `/blog/abc` to `/posts/abc`.

### Conclusion:

The Next.js Pages Router simplifies routing by using the file system as the routing mechanism. You can create nested, dynamic, and custom routes easily and navigate between them using the `Link` component. Additionally, you can access router information using the `useRouter` hook and customize route behavior using special functions like `getStaticProps` and `getServerSideProps`.
