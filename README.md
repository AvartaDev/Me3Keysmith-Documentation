# Me3Keysmith-documentation

This repository holds the public documentation for the Me3Keysmith documentation.

The structure of the repository is made such that it can be used with Github Pages.

This means that the directory _docs_ is reserved for Github Pages.

The source code is located in the directory _documentation_. Docusaurus is the tool used to generate the documentation.

## Generating the documentation

The documentation can be generated in development mode or production mode. Regardless of the option, you need to go into the directory:

```bash
cd documentation
```

To create the documentation in development mode:

```bash
npm start
```

To create the documentation in production mode (i.e. to be published using Github Pages):

```bash
npm run build
```

> You can check that the production build is correct by running `npm run serve` locally.

## Developer Notes

There are two branches for this repository: `main` and `gh-pages`.

`gh-pages` is the branch that is used to publish the documentation. The _.gitignore_ file in this branch is slightly different from the one in the `main` branch in that the _docs_ directory is not ignored.

It is necessary for the _docs_ directory to be present in the `gh-pages` branch as Github Pages uses that to serve as the publicly accessible documentation site.
