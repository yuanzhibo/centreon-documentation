To understand how the documentation is structured, you may have a look to the
 [Docusaurus project](https://docusaurus.io/).
We're using version 2.

### Pull request guidelines

Help us review your PRs more quickly by following these guidelines.

* Try not to touch a large number of files in a single PR if possible.

* Don't change whitespace or line wrapping in parts of a file you are not editing for other reasons. Make sure your text editor is not configured to automatically reformat the whole file when saving.

### Style guide

Try not to have lines over 80 characters. Use your best judgment, and try to follow the example
set by the existing documentation.

## How to build the documentation locally

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator.

### Which branch should I base my PRs on?

Use branch **staging**. We will merge the PR into production once it has gone through the validation process.

### Prerequisites

1. Install **yarn**. On Windows: https://classic.yarnpkg.com/latest.msi

2. Install **node.js** (version 14 minimum): https://nodejs.org/en/download/

3. Clone the repository :

   ```
   git clone https://github.com/centreon/centreon-documentation.git
   ```

4. If you need, create and/or check out the branch you want:

   ```
   git branch <name_of_branch>
   ```

   ```
   git checkout <name_of_branch>
   ```

4. Install dependencies:

   ```
   yarn install --frozen-lockfile
   ```

### Building the documentation website

* Build the EN or FR version of the site (faster)

   * EN: ```yarn start```
   * FR: ```yarn start --locale=fr```

   The website opens in your browser at the following address: http://localhost:3000/. Most changes are reflected live without having to restart the server.

* If you really need to build the whole website, use the following command (but be aware it takes a long time to build):

   ```
   yarn build
   ```

   Then use the `npm run serve` command to open the website in your browser.

## Adding files to the table of contents

* There is only 1 ToC file per version, in English. ToC files are located in the **versioned_sidebars** folder. For instance, the EN ToC file for version 21.10 is called **version-21.10-sidebars.json**.
* For the French ToC, there is no ToC file, but a .json file which contains translated strings for chapter headings, located in the following folder: **i18n\fr\docusaurus-plugin-content-docs**. For instance, the FR translation file for version 21.10 is called **version-21.10.json**.

## Making changes to the same file in different versions

If you want to make the same change to a file across different versions, you have to copy your change to each version of the doc manually (no cherrypicking).

## Docusaurus documentation

If you need help with Docusaurus, read their [documentation](https://docusaurus.io/docs).
