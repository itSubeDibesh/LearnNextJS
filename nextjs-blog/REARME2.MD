# Day2(NextJs-Blog)

[π Back to Day1](README.md)

## Things Learnt

- Pre-rendering has everything rendered before Hydration whereas No Pre-rendering renders everything after hydration but interactivity depends on whether js has been loaded.
- Pre-rendering is further classified into two forms
  - Static Generation(With/Without data) : HTML generated on build time
  - Server-side Rendering : HTML generated on each request
- Pages in Next can be configured in hybrid mode meaning we can use both Static generation and Server-Side Rendering based on requirements
- Prioritize using Static Generation for better experience
   `You should ask yourself: "Can I pre-render this page ahead of a user's request?" If the answer is yes, then you should choose Static Generation.`

### Static Generation with Data using getStaticProps

Essentially, getStaticProps allows you to tell Next.js: ___βHey, this page has some data dependencies β so when you pre-render this page at build time, make sure to resolve them first!β___

```typeScript
export default function Home(props) { ... }

export async function getStaticProps() {
  // Get external data from the file system, API, DB, etc.
  const data = ...

  // The value of the `props` key will be
  //  passed to the `Home` component
  return {
    props: ...
  }
}
```

π In development mode, `getStaticProps` runs on each request instead

π `getStaticProps` only runs on server side and is only allowed on page

### Server-Side Rendering with getServerSideProps

Because getServerSideProps is called at request time, its parameter (context) contains request specific parameters.

```typeScript

export async function getServerSideProps(context) {
  return {
    props: {
      // props for your component
    },
  };
}
```

You should use getServerSideProps only if you need to pre-render a page whose data must be fetched at request time. Time to first byte (TTFB) will be slower than getStaticProps because the server must compute the result on every request, and the result cannot be cached by a CDN without extra configuration.

πUse of tools like SWR helps to enhance CSR(Client side Rendering)
