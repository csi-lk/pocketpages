# File-Based Routing in PocketPages

PocketPages supports file-based routing, allowing you to create a clean and intuitive URL structure directly from your file and folder organization. This guide will discuss how to set up file-based routing using a nested directory structure, ensuring your application's URLs align with the layout of your EJS files.

## Understanding File-Based Routing

File-based routing means that the URLs in your application are automatically determined by the file and folder structure within the `app/pb_hooks/pages` directory. Each `.ejs` file corresponds to a unique route, and the nested folders reflect URL paths.

### Basic Example

Consider the following directory structure:

```
app/
  pb_hooks/
    pages/
      index.ejs
      about.ejs
      contact.ejs
      products/
        index.ejs
        details.ejs
        reviews/
          index.ejs
          latest.ejs
```

### How the Routing Works

- **Root-Level Routing**:

  - `index.ejs` at the root level (`app/pb_hooks/pages/index.ejs`) is served at the root URL `/`.
  - Other root-level `.ejs` files like `about.ejs` and `contact.ejs` are served at `/about` and `/contact`, respectively.

- **Nested Routing**:

  - The `products/` folder represents the `/products` URL path.
  - `products/index.ejs` is served at `/products`. If no other file in the `products/` directory matches the URL, this `index.ejs` file is used by default.
  - `products/details.ejs` is served at `/products/details`.

- **Deeper Nesting**:
  - The `reviews/` folder inside `products/` represents the `/products/reviews` path.
  - `products/reviews/index.ejs` is served at `/products/reviews`.
  - `products/reviews/latest.ejs` is served at `/products/reviews/latest`.

### Special Cases - `index.ejs`

As mentioned, `index.ejs` files have a special role:

- **Default Route Handling**: If a user visits a path like `/products` and there is an `index.ejs` file within that folder (`app/pb_hooks/pages/products/index.ejs`), this file will be served without the need for specifying `/products/index` in the URL.
- **Root Page**: The `index.ejs` at the root of `app/pb_hooks/pages/` serves as the homepage (`/`).

### Example Directory and Routes

Let’s break down the example directory structure with corresponding routes:

- **Root Level**

  - `app/pb_hooks/pages/index.ejs` -> `/`
  - `app/pb_hooks/pages/about.ejs` -> `/about`
  - `app/pb_hooks/pages/contact.ejs` -> `/contact`

- **Products**
  - `app/pb_hooks/pages/products/index.ejs` -> `/products`
  - `app/pb_hooks/pages/products/details.ejs` -> `/products/details`
  - `app/pb_hooks/pages/products/reviews/index.ejs` -> `/products/reviews`
  - `app/pb_hooks/pages/products/reviews/latest.ejs` -> `/products/reviews/latest`

## Tips for Structuring Your Routes

1. **Keep It Organized**: Reflect the logical structure of your application within your directory layout. For example, if you have sections of your site dedicated to products, services, and contact information, create corresponding folders in `app/pb_hooks/pages/`.

2. **Use `index.ejs` for Default Pages**: Utilize `index.ejs` within any folder to create a default route for that path. This helps simplify URLs, making them more user-friendly.

3. **Deep Nesting for Complex Structures**: For applications with more complex navigation, use deep nesting. Ensure that each folder only contains related pages to maintain clarity in your routes.

4. **Avoid Over-Nesting**: While nesting is powerful, avoid creating unnecessarily deep structures. This can lead to cumbersome URLs that are hard to navigate and remember.

### PocketPages Routing Priority

In PocketPages, the routing system is designed to take precedence over any default PocketBase routes and static files served from the `pb_public` directory. This means that if a route or file exists both in PocketPages and PocketBase, the PocketPages route will be served instead.

This behavior occurs because the PocketPages middleware runs first, ensuring that your custom routes, dynamic content, and EJS templates are always prioritized over default PocketBase routes or static content.

#### Example Scenario

- **PocketPages Route**: You have an EJS file located at `pb_hooks/pages/about/index.ejs`.
- **PocketBase Route**: There is a static HTML file located at `pb_public/about.html`.

When a request is made to `/about`, the PocketPages route (`index.ejs`) will be served, even though there is a static file in `pb_public`.

### Key Points

- **Middleware Execution Order**: The PocketPages middleware is executed before PocketBase handles any routes or serves static files, ensuring your PocketPages routes always take priority.
- **Routing Conflicts**: If you have a route defined in both PocketPages and PocketBase, the PocketPages version will be served.

This routing priority ensures that your custom logic and dynamic content in PocketPages are always prioritized, giving you full control over the routing and content delivery in your application.

## Summary

### Updated Summary

File-based routing in PocketPages allows you to effortlessly create intuitive and well-structured URLs by organizing your EJS files and folders within the `app/pb_hooks/pages` directory. By following the directory structure, your application’s routing will naturally align with your layout, making it easy to manage and scale.

In addition to providing a clear and organized routing system, PocketPages routes take precedence over any default PocketBase routes or static files in the `pb_static` directory. This ensures that your custom logic, dynamic content, and EJS templates are always prioritized, giving you full control over the routing and content delivery in your application.

Whether you’re building a simple site with a few pages or a complex application with multiple nested sections, PocketPages' file-based routing offers a straightforward and efficient way to map your content to URLs, ensuring that your application's routing behaves exactly as you intend.