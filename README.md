## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

### Notes

```
/app: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.

/app/lib: Contains functions used in your application, such as reusable utility functions and data fetching functions.

/app/ui: Contains all the UI components for your application, such as cards, tables, and forms. To save time, we've pre-styled these components for you.

/public: Contains all the static assets for your application, such as images.

/scripts: Contains a seeding script that you'll use to populate your database in a later chapter.
Config Files: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app. You will not need to modify them in this course.
```

## layouts and pages

- page.tsx : special next.js file exports a react component. Only this is public
- layout.tsx : to create UI that is shared between multiple pages, partial rendering!

## client side component

- hooks, use\*

## Server Side components

- Allows use of sql directly to query

## redering

### static rendering

With static rendering, data fetching and rendering happens on the server at build time (when you deploy) or during revalidation. The result can then be distributed and cached in a Content Delivery Network (CDN).

Whenever a user visits your application, the cached result is served. There are a couple of benefits of static rendering:

- Faster Websites - Prerendered content can be cached and globally distributed. This ensures that users around the world can access your website's content more quickly and reliably.

- Reduced Server Load - Because the content is cached, your server does not have to dynamically generate content for each user request.

- SEO - Prerendered content is easier for search engine crawlers to index, as the content is already available when the page loads. This can lead to improved search engine rankings.

Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data that is regularly updated.

### dynamic rendering - limited by the server request

With dynamic rendering, content is rendered on the server for each user at request time (when the user visits the page). There are a couple of benefits of dynamic rendering:

- Real-Time Data - Dynamic rendering allows your application to display real-time or frequently updated data. This is ideal for applications where data changes often.

- User-Specific Content - It's easier to serve personalized content, such as dashboards or user profiles, and update the data based on user interaction.

- Request Time Information - Dynamic rendering allows you to access information that can only be known at request time, such as cookies or the URL search parameters.

## STREAMING! - move data fetching down to component level, use suspense

Streaming is a data transfer technique that allows you to break down a route into smaller "chunks" and progressively stream them from the server to the client as they become ready.

By streaming, you can prevent slow data requests from blocking your whole page. This allows the user to see and interact with parts of the page without waiting for all the data to load before any UI can be shown to the user.

- skeleton component
- suspense
- react group (folder)

## search + pagination

When to use the useSearchParams() hook vs. the searchParams prop?

You might have noticed you used two different ways to extract search params. Whether you use one or the other depends on whether you're working on the client or the server.

<Search> is a Client Component, so you used the useSearchParams() hook to access the params from the client.

<Table> is a Server Component that fetches its own data, so you can pass the searchParams prop from the page to the component.
As a general rule, if you want to read the params from the client, use the useSearchParams() hook as this avoids having to go back to the server.

## server actions - https://nextjs.org/learn/dashboard-app/mutating-data

**Chapter Focus: Data Mutation with Next.js**

This chapter dives into how to use Next.js to handle changes to your application's data, such as creating, updating, and deleting information. Key techniques involved are:

- **Server Actions:** Next.js's streamlined way to handle data mutations server-side for enhanced security and performance.
- **Forms and Form Handling:** HTML forms, their interaction with Server Actions, and how to use React's `action` attribute.
- **Client-Side Caching with Next.js:** How Next.js caches data for faster access and the `revalidatePath` function to update stale data.

**Key Concepts and Explanations**

1. **Server Actions**

   - **What:** Asynchronous functions executed directly on the server. Perfect for sensitive data operations, secure interactions with databases, and reducing the amount of client-side JavaScript needed.
   - **Benefits:**
     - **Security:** Data manipulation happens on the server, reducing vulnerability to attacks like Cross-Site Scripting (XSS).
     - **Performance:** Offloading data processing to the server can improve app responsiveness.
     - **Progressive Enhancement:** Forms with Server Actions can work even if JavaScript is disabled.
   - **Integration:** Server Actions create backend API endpoints automatically, so you don't need to write them manually.

2. **Forms with Server Actions**

   - **The `action` Attribute:** In regular HTML, the `action` attribute in `<form>` points to an API endpoint. In Next.js with Server Actions, it calls the Server Action directly.
   - **Submitting Data:** Submitting a form invokes the Server Action, which automatically receives a `FormData` object containing the form's data.

3. **Data Extraction, Validation, and Transformation**

   - **The `formData.get()` Method:** Used to extract values from the `FormData` object in your Server Action.
   - **Validation with Zod:** Zod is a TypeScript library that simplifies data validation to ensure correct data types before persisting them in your database.
   - **Preparation for the Database:** Your Server Action likely needs to format data (e.g., converting numerical strings to numbers, storing money in cents for accuracy, and generating dates) before saving.

4. **Inserting Data into the Database**

   - **SQL Queries:** Server Actions interact with databases using SQL queries. Your SQL syntax will depend on the specific database you're using.
   - **Error Handling:** Production code should always include robust error handling around database operations to handle unexpected issues.

5. **Cache Revalidation with `revalidatePath`**

   - **Why it Matters:** After data changes, your Next.js app needs to refetch updated data from the server.
   - **How It Works:** `revalidatePath` invalidates the client-side cache for a specific route, ensuring the next visit will fetch fresh data.

6. **Redirection with `redirect`**

   - **Purpose:** After data changes, it's customary to redirect the user to another page, such as a success message or a list view.
   - **Functionality:** The `redirect` function handles URL redirection in Server Actions.

**Additional Considerations & Best Practices**

- **Accessibility:** Ensure your forms are accessible by providing labels, appropriate error messages, and good structure for screen readers.
- **User Experience:** Provide clear feedback mechanisms (loading states, success/error messages) to keep the user informed of the actions' progress.
