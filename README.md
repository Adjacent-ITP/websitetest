# Workflow WIP

This is a work in progress. It assumes you have Hugo set up locally, and have cloned this repo. Proper branching hasn't been setup yet, amongst other things.



## Creating a new issue:

To create a new Adjacent Issue, lets say `issue-X`, follow these steps:

1. **Create assets directory:** `/assets/_issue-template` and change the name of the new folder to `issue-X`.

   i.e, you will have this:

   ```
   /assets
   |--- common
   |--- landing-page
   |--- _issue-template
   		|--- scripts
   		|--- styles
   |--- issue-X
   		|--- scripts
   		|--- styles
   ```

   The new directory is where you will store all `css` and `js` needed for the issue. `/styles` is set up to use `scss`/`sass` by default


2. **Create template directory:** Duplicate `/layouts/_issue-template` and change the name of the new folder to `issue-X`.

   i.e, you will have this:

   ```
   /layouts
   |--- _default
   |--- _issue-template
   		|--- baseof.html
   		|--- list.html
   		|--- single-alt.html
   		|--- single.html
   |--- issue-X
   		|--- baseof.html
   		|--- list.html
   		|--- single-alt.html
   		|--- single.html
   ```

   The new directory is where you will store all the template files related to the issue.

   * The  `baseof.html` file defines the basic HTML structure
   * The  `list.html` file will be used to list all the articles in the issue, ie, the issue's landing page
   * The  `single.html` file is the layout for an article / single post
   * The  `single-alt.html` file is an alternative layout for an article

   Any number of additional article templates can be created, and each article can specify which one should be used.



3. **Create content directories:** Using the Command Line Interface, enter this command to create a content folder for the issue (assuming this is `issue-X` again):

   ```
   hugo new --kind issue-bundle issue-X
   ```

   Create directories for each article like so, putting in the article title (can be changed later):

   ```
   hugo new --kind article-bundle issue-X/a-great-article-title
   ```

   ```
   hugo new --kind article-bundle issue-X/another-article-at-the-intersection
   ```



4. Launch the server from the command line and you should see content

   ```
   hugo server
   ```

---

<br>
<br>



## Workflow for editors

Editors can use Github's GUI for editing, following these steps (will be modified to be permission-based soon)

1. Ensure you are on the `editors` branch -- use the `Branch` drop down on the top left above the file tree *(this step needs to be eliminated)*
2. *To add text:*
   * Navigate to the article you need to update -- `/content/issue-X/article-title/_index.md`
   * Click on the edit icon (pencil on top right) to edit. Use markdown syntax, and preview mode for feedback.
   * When you are done, add a commit message -- be descriptive -- ensure you select **"commit directly to the `editors` branch"**
3. *To add images*:
   * Navigate to the article you need to update -- `/content/issue-X/article-title/assets`
   * Click on the `Upload File` button (on top right). Drag your file in
   * When you are done, add a commit message -- be descriptive -- ensure you select **"commit directly to the `editors` branch"**
   * Uploaded images will not automatically appear, edit the `_index.md` file to link them like so `{{< figure src="assets/myImage.jpg" >}}` (*a document of this and other shortcuts will be compiled*)

---


<br>
<br>

## Deployment

* There will be 4 active branches --  `development`, `staging`, `production` and `editors`
* Dev work will be carried out on `development`.
* Editors change the `editors` branch, and developers can merge changes into `development` as needed
* `development` will be merged into `staging`; and `staging` into `production` as needed (only one-directional)
* There will be 2 remote repos
  * `github` which refers to the repo stored on github, used for collaboration.
  * `server` which refers to a bare repo stored on Shawn / ITP's servers

* Using `post-receive` hooks on `server`, (sample file `post-receive.sample`), the branch will be extracted to the correct directory
* A `deploy` script can be used to rebuild the site and push it to `server`
* On publishing a new issue, the git history can be deleted, to save bloat from images

---

<br>
<br>


## TODO:

* Deployment workflow / server access
* Github permissions / limit GUI access to `editors` branch
* Create partials for common UI elements
* Create documentation for editors on partials / front matter etc
