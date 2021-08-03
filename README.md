# Reliably Documentation with Gridsome

This is the <a href="https://reliably.com/docs/">Documentation for Reliably</a>, built with <a href="https://gridsome.org" target="_blank" rel="noopener noreferer">Gridsome</a>.

## Contribute

### Requirements

To contribute to this repository, you should have the following installed:

* [`Node 14.*`](https://nodejs.org/en/) (We'd recommend using [`nvm`](https://github.com/nvm-sh/nvm) to manage Node versions - We include a `.nvmrc` file to specify the version)

### Steps
1. Install the dependencies with `npm install`.
2. Run `npx gridsome develop` to start a local dev server at `http://localhost:8080`
3. Happy coding 🎉🙌

If you wish to contribute to this documentation, please submit a PR with your changes for review.

## Notes

### Links in Markdown

The standard way to create links in Markdown is as follow: `[anchor](/some/documentation/page/)`.

While this works, it should be used only for external links. This notation is converted to _regular_ links: `<a href="/some/documentation/page/">anchor</a>` and does not benefits from Gridsome's ability to pre-fetch links.

You should prefer Gridsome's `<g-link>` component, and use it this way: `<g-link to="/some/documentation/page">anchor</g-link>`

As a sidenote, it is recommended that if you choose to open an external link in a different tab (which some consider bad practice) with the `target="_blank"` attribute, you also you the `rel="noopener noreferer"` attribute. As this attribute is not supported by the Markdown link notation, you should in this case rely on a standard link: `<a href="https://example.com" target="_blank" rel="noopener noreferer">Click here!</a>`.