# Smart Tools Documentation Process

## When does content authoring start for a release?

In general, content authoring starts after all stories to be included in a given project release have been selected. The content authoring process begins with analyzing stories for docs impact and information gathering. Most Smart Tools stories include a fair amount of feature spec info, links to design mockups, and other supporting information, so actual writing can start at any time after a story has been added to a project release. Typically, a new release cycle begins the day after the previous release has gone to production.

To generate a complete list of stories for the release, create a Jira search filter with the following values:

-  **Project:** Citrix Smart Tools
-  **Type:** Story
-  **Status:** All
-  **Assignee:** All
-  **Fix Version:** Select the target release.

## How is content authoring tracked for each feature story?

The author performs the following actions:

-  Analyzes each story and estimates the impact to documentation.
-  Creates a documentation story in Jira that can be tracked alongside all other stories in the release. All documentation subtasks are attached to this story. This story includes the following information:
    -  **Title:** Use the format "Documentation for `Release-Name`."
    -  **Priority:** If the release contains new features or significant enhancements to existing features, select **Major**. Otherwise, leave unset.
    -  **Label:** None.
    -  **Fix Version:** Select the target release.
    -  **Description:** Enter a basic summary or leave blank.
-  Creates documentation subtasks in Jira and links them to the documentation story for the release. Each sub-task includes the following information:
    -  **Title:** Use the format "Doc Task: `Task-Title`."
    -  **Priority:** Should match the priority of the feature story, if set.
    -  **Label:** Select **Doc_Tracking**. If it's related to a specific Smart Tools feature like Smart Scale or Smart Check, also add appropriate labels (e.g., "smartscale", "smartcheck", "smartbuild", etc.)
    -  **Fix Version:** Select the target release.
    -  **Description:** Enter a detailed description of the docs plan for covering the feature. For example, specify if new topics will be created, any existing articles that are affected, and the scope of effort required.

Progress on doc tasks is signaled as follows:

-  When work begins on a doc task, click **Start Progress** to change the status to "In Progress."
-  When content for a doc task has completed the review process, click **Resolve** to change the status to "Resolved."
-  When the content addressing an issue has been published, click **Close** to change the status to "Closed."
-  While working the doc task, add comments as necessary so others on the team are aware of past and ongoing progress.
-  If subject-matter questions arise during the writing process, the quickest way to reach out is to @mention the relevant people working the story in a comment in Jira (the bulk of discussion happens in story comments). If in doubt, consult the Product Manager.

The author can keep track of unfinished doc tasks by using the **Issues > My Open Issues** filter. If additional information needs to be included in the filter, the author can create a custom search filter and include the relevant fields.

## How are topic reviews performed?

Content items are submitted for review immediately after the item has been completely drafted. A "complete" draft is a new or updated article that adequately addresses the story to which it applies. However, due to Smart Tools' compressed release cycles, "complete" might be interpreted as "complete as of right now." It's not uncommon for the final implementation of a story to have slightly different capabilities or to look a little different than originally specified – changes which can occur after a content item has been reviewed. So, the author should actively monitor doc-related stories to keep abreast of any issues or design changes, and recheck the product test environment to verify the content is still accurate.

Topic reviews are conducted through Confluence. The author creates a new folder under **Smart Tools Topic Reviews** and creates new pages with the content to be reviewed. Depending on the content item to be reviewed, the author adds the content of the entire article (if new or to provide context for an update) or just the section to be added or updated. The author then sends out a request (using email, Slack, or other notification type) to all the reviewers for feedback. Reviewers should provide feedback on the Confluence page, either as a page comment or an inline comment, so feedback can be tracked & archived.

Due to the compressed release schedules for Smart Tools, "content reviews" (peer-author reviews for style and copy) and "technical reviews" (SME reviews for technical accuracy) are performed concurrently. Content reviews are optional, depending on the experience level of the writer (for new writers, content reviews are required) However, technical reviews are always required.

When opening review sessions, use email and Slack to notify the following people:

-  Smart Tools Product Manager
-  Smart Tools Development Manager
-  Smart Tools Release Manager
-  Any developers or testers involved in implementing and testing the feature story

Depending on the length of the content item to be reviewed and the number of items submitted at any given time, reviewers should be given up to a week to provide review feedback.

If no reviewers provide feedback or signal approval during the review period, the author sends another notification, indicating no content will be published in the absence of feedback or approval. If no feedback or approval is received from the Smart Tools PM when the release goes to production, a final notification is sent to all reviewers indicating no content has been published for the release and including a final request to review. If no feedback or approval is received, include the unpublished content in the next release's review.

## Documentation repository

Smart Tools documentation is maintained using Zendesk, a paid SaaS helpdesk product that includes knowledge base article authoring capabilities. Citrix uses only the article authoring capabilities to create the Smart Tools doc set. Also, the Smart Tools documentation web site is designed only to provide official product documentation. Citrix does not use any of Zendesk's community or helpdesk features to resolve issues or encourage customer interaction. Instead, customers use the Citrix Smart Tools support forum to ask questions and register feedback.

## Content authoring and publishing

The Smart Tools content authoring process is as follows:

1.  Create an article in the Smart Tools Sandbox category and add content. The Sandbox category ensures the in-progress article is kept separate from published docs to avoid accidental publishing.
1.  Submit the article for review to SMEs.
1.  Incorporate review feedback into article.
1.  Stage the article for publishing.
1.  On the release date, publish the article.

    > Note
    >
    > "Release date" means the date on which the product updates have been pushed to production. It is common for a Smart Tools releases to be scheduled for a certain date, but change at the last minute. The author should continually verify the actual release date with the Product Manager throughout the cycle, as such changes are not always communicated to all stakeholders.

### Authoring draft content

Although Zendesk comes with a WYSIWYG editor, authors should use a separate HTML editor to draft content for new topics or to perform significant editing of existing articles. The Zendesk editor is suitable for most "lite" editing and text formatting, but has the following limitations:

-  It does not provide a friendly way to structure content with headings. To do this, authors must manually enter the appropriate heading tags in the HTML source.
-  It does not produce HTML that renders predictably when the article is published. Zendesk often injects additional code when formatting, creating tables, or creating multi-level lists that some browsers might not render properly.
-  It does not provide a friendly way to invoke CSS formatting for a selected paragraph. For example, to format a paragraph as a note, the author must add the `note` class (defined in the doc site's CSS) to the `<p>` tag in the HTML source.

As an alternative to the Zendesk editor, use any of the following options to draft new content or edit existing articles:

-  **Adobe Dreamweaver:** Most authoring teams have access to Adobe Creative Cloud, so this is a ready-made option to take advantage of.
-  **Kompozer:** This is a free and open source WYSIWYG HTML editor with simple formatting and editing capabilities. For more information, see <http://kompozer.net/>.
-  **Bluegriffon**: Another open source WYSIWYG HTML editor with a few more bells and whistles. Generally free to use, but access to documentation requires a paid license. For more information, see <http://bluegriffon.org/>.

> Important
>
> If you want to use word-processing programs such as Microsoft Word to draft or edit content, be aware the output of these programs is not Zendesk-friendly. You might need to hand-code the HTML equivalent of any styles you use and re-insert any images you added.

Tips for copying and pasting content between Zendesk and your editor of choice:

-  Copy and paste entire articles only. It's a lot easier to make sure your edits are captured faithfully in Zendesk, rather than hunting and pecking for each updated bit.
-  Copy and paste the HTML source only. In the Zendesk editor, click the **Source** button to view the article's HTML source. Zendesk's source editor displays only the code that appears between the `<body>` tags of an HTML document.
-  When using a separate editor, paste HTML source from Zendesk into the Source view of your editor. Make sure you paste between the `<body>` tags in your editor.

### Keeping draft content private until release

In Zendesk, authors can designate an article "published" or "draft." In general, published articles are viewable by the entire world while draft articles are viewable only by authors.

The "Draft" designation keeps an article private in that it does not appear in any section to which it might be assigned. To access the article, you can:

-  Click **Help Center admin > Drafts**, or
-  Note the article's URL when you save the draft and then enter it in your browser's address bar when needed.

Although the "Draft" designation makes it easy to keep draft content private within a public section of the Smart Tools docs site, authors should instead publish draft-mode content to the Smart Tools Sandbox and manage the authoring process from there.

The Smart Tools Sandbox is a private category in Zendesk, so all the articles with the "Published" designation are viewable in the category's contents, but only for logged-in Zendesk users. Using the Smart Tools Sandbox is preferable because:

-  It's easier to manage publishing of draft content that forms an entire new section in the doc set (e.g., for a new feature like Smart Check or Smart Scale).
-  Changing a currently-public article from "Published" to "Draft" effectively hides it from customers. So, it's not a good method to use for making updates to an existing article for a specific release. Since we expect the article to remain available to customers while we update it, it's better to copy it to the Smart Tools Sandbox, work on the updates from there, and then copy the completed updates back to the original article.

To make the sandbox content truly public for customers, the content is moved from the private Smart Tools Sandbox category to the appropriate section in the public Documentation category.

### Linking to other Smart Tools sections and articles

URLs in Zendesk use the following format:

-  For sections: `http://manage-docs.citrix.com/hc/en-us/section/*SectionID-Section-Title*`
-  For articles: `http://manage-docs.citrix.com/hc/en-us/articles/*TopicID-Topic-Title*`

In general, having the titles in URLs is key to ensuring content can be found online. Google, in particular, places a lot of relevancy weight on titles and how closely they match the actual title of the page and its content. By default, Zendesk creates URLs that are search engine friendly since they include the exact title of the section or article. When the title is changed, Zendesk updates the display of the URL in the browser the next time the page is accessed.

#### When NOT to use the title in the URL

When linking to sections or articles in Zendesk, DO NOT USE the entire URL. Instead, copy the URL and delete the title portion. For example:

-  **Use this URL:** `https://manage-docs.citrix.com/hc/en-us/articles/212714943`
-  **Don't use this URL:** `https://manage-docs.citrix.com/hc/en-us/articles/212714943-Update-delivery-controllers-and-machine-catalogs-in-a-XenApp-and-XenDesktop-site`

This applies to all situations and circumstances where a link is needed. This includes in-product links, links from other product doc sets, marketing newsletter links, internal sharing amongst employees, and social media shares.

> Important
>
> Zendesk doesn't use the section or article title to locate the target of a link – only the ID. This allows authors to change titles as necessary without breaking links elsewhere.

#### Why don't we use the entire URL in links?

-  Because some titles are longer than others, the URL can get unwieldy when moused over and displayed as a tooltip or in the lower left corner of the browser.
-  Including the title in the URL can result in links that look old and can't always be updated timely. If a public article is updated with new information for a release, and the title is changed to suit those updates, any links to that article will continue to show the old title. This can have the following effects:
    -  Customers might think they're on the wrong page. The title in the URL can set an expectation that the article will display that same title. If the actual title is markedly different, it's possible customers might assume they've been redirected (which can alarm some security-minded customers), their link is wrong, or the intended page has been removed.
    -  The maintenance overhead on the Dev side increases. If an in-product ("Learn More") link includes the title and the title is updated, getting that in-product URL updated with the new title might not happen when it should, as this is a very low priority task for Dev.
    -  The maintenance overhead on the authoring side increases. Links between Smart Tools sections or articles are not automatically updated when titles change. These links must be located and updated manually.

Dropping the title from the URL helps ensure links look evergreen, stay at a relatively uniform length, and minimize the maintenance work that might be required.

### Create or update an article in the Smart Tools Sandbox

To create a new article:

1.  Create an article in the **Smart Tools Sandbox** category. If the article is an out-of-band topic that isn't tied to a particular release, add it to the **New Topics** section. If the article is tied to a release, add it to the section dedicated to that release.
1.  Title the article using the format `Content-Status - Jira-ID: New-Article-Title`.
1.  Add content to the article and save.
1.  Change the status of the article from **Draft** to **Publish**.

> Note
>
> Even though the article is published, it's still hidden from customers while it remains in the Smart Tools Sandbox.

To update an existing public article for a release:

1.  Create an article in the **Smart Tools-Sandbox** category. If it's an out-of-band update, add it to the **Existing topics** section. If the update is tied to a release, add it to the section dedicated to that release.
1.  Copy the entire contents from the existing public article and paste it into the sandbox article.
1.  Title the sandbox article using the format `Content-Status - Jira-ID: *Existing Article Title`.
1.  Update the content in the sandbox article as needed.

> Important
>
> Do not change the status of an existing public article to "Draft" to update it. This hides the article from customers until it is changed back to "Published." For quick spot-updates (e.g., correcting a typo, etc.), simply update the public article in-place.

Additional information:

-  `Content-Status` refers to the current authoring status of the article. The status for all sandbox articles in the writing state is "In Progress."
-  `Jira-ID` refers to the Jira issue ID of the doc task that addresses a specified story included in the release.
-  `New-Article-Title` is the article title for the new content.
-  `Existing-Article-Title` is the title used in the currently published article.

### Submit the article for review

1.  In Confluence, create a folder for the release under the [Smart Tools Topic Reviews](https://no-url.html).
1.  Create a new document in the release folder and copy and paste the drafted content item. Also, perform the following actions:
    -  Reinsert any screenshots, if applicable.
    -  Reformat any text, sections, or headings as needed.
    -  Remove any in-topic navigation such as "Back to top" links or table of contents links.
    -  Change the text color of all drafted content changes to orange, so reviewers can zero in on what's been added or changed for the release.
    -  Add a Note macro at the top of the document including the following:
        -  The existing published topic, if any, to which the updates apply (include link)
        -  The Jira ticket(s) that the updates address (include links)
        -  Boilerplate for reviewers with items to keep in mind during review
1.  Draft an email to notify recipients the review session is open and send to the following people:
    -  Product Marketing
    -  Product Management
    -  Smart Tools Designer(s)
    -  Smart Tools Dev Release Manager
    -  Smart Tools Development Lead
    -  Smart Tools Test Lead
    -  Any peer authors on the Smart Tools team or on other product teams who can devote some time to provide content review feedback.
1.  In Zendesk, change the `Content-Status` value of the sandbox article to **Review** to indicate the article is in the review process.
1.  When feedback has been received from reviewers, update the sandbox article accordingly.

### Stage the article for publishing

1.  In Zendesk, perform a careful "last-stage" review of the sandbox article. Remove any author's notes or placeholders, and correct spelling, grammar, and punctuation as needed.
1.  Change the `Content-Status` value to **Publish**. This indicates the article is ready to be published on the release date.

### Publish the article

To publish a new article:

1.  Remove the `Content-Status` and `Jira-ID` values from the title.
1.  Change the category location of the article from `Smart Tools Sandbox > Section-Title`" to the appropriate section of the **Documentation** category. To publish all the articles in a new section all at once, change the category of the section from **Smart Tools Sandbox** to **Documentation**.

To publish an update to an existing public article:

1.  Copy the entire contents of the sandbox article.
1.  Edit the public article in the "Documentation" category and select the entire contents.
1.  Paste the contents of the sandbox article to the public article.
1.  If the article title was updated in the sandbox article, update the title of the currently published article to match. DO NOT include the `Content-Status` or `Jira-ID` values in the published article's title.
1.  Click **Update**.
1.  If the article contains screenshots, load the updated published article in a separate browser and verify all the screenshots appear when the page is loaded. For example, if you use Google Chrome to author in Zendesk, load the published updated page in Internet Explorer or Mozilla Firefox to perform the verification.

### Re-arrange articles

After moving published articles to a particular Documentation section, the article typically appears at the top or bottom of the section's article list. Re-arrange this list so the sequence of topics makes sense to customers.

1.  From the Help Center toolbar, click **Articles > Arrange articles**.
1.  Expand the **Articles** section and then expand the section you want to arrange. If you need to move a topic to a different section, expand the destination section as well.
1.  Point to the topic you want to move and then drag it to the target location.
1.  Click **Save**.

### Back up published content

After articles have been published for a release, create a backup of all the articles in the doc set. This ensures Citrix has a current archive of published topics at any given time. For instructions, see the [Content Backups](https://no-url) Confluence page.

## Special Cases

### Smart Check Alerts Reference

The Smart Check Alerts Reference article contains the entire collection of Smart Check alerts content in a single table. Updating this article involves creating HTML output of the master alerts spreadsheet and copying the HTML table code to the article in Zendesk.

> Note
>
> Be aware that the Smart Check Alerts Reference article is very long, so Zendesk will be a bit slow when editing and saving the article.

#### To update the Smart Check Alerts Reference

1.  Save a copy of the master alerts spreadsheet:
    1.  Navigate to the [Alerts](https://no-url.html) page and, in the far right corner, click the menu button. Select **Attachments**.
    1.  On the Attachments view, expand **cleanAlerts.xslx**, right-click on the latest version, and select **Save link as**.
1.  Convert the spreadsheet to HTML:
    1.  Open the spreadsheet in Microsoft Excel.
    1.  Delete the **Notes** and **Reviewer** columns. These are internal-only fields that we don't expose to customers.
    1.  Click **File > Save As** and select the folder where you want to save the HTML output. The Save As dialog appears.
    1.  In **Save as type**, select **Web Page (\*.htm; \*.html)**.
    1.  In **Save**, select **Selection: Sheet** and then click **Save**.

        > Note
        >
        > You must select **Selection: Sheet** for Excel to save the spreadsheet as an HTML table. If you simply save the entire workbook, the output won't include any HTML table output.

    1.  When prompted, click **Publish**. Excel converts the spreadsheet to HTML and saves it to the location you specified.
1.  Edit the HTML table code:
    1.  In a text editor, open the HTML file you just saved.
    1.  Locate the `<table>` tag and change the "border" attribute to "1."
    1.  Locate the first `<td>` tags that contain column heading text such as "ID," Title," "Description," and so on.
    1.  For each column heading, change the beginning and ending `<td>` tags to `<th>`. For example: `<th>ID</th>`
    1.  Select and copy everything between the `<table`> and `</table>` tags.
1.  Replace the table in Zendesk:
    1.  Log on to Zendesk, navigate to [https://manage-docs.citrix.com/hc/en-us/articles/115000817343](https://manage-docs.citrix.com/hc/en-us/articles/115000817343-Smart-Check-alerts-reference), and click **Edit article**.
    1.  Click the **Source code** button and select everything between the `<table>` and `</table>` tags.
    1.  Paste the table code you just copied, replacing the selected HTML table.
    1.  Click **Update**.

## How are assets managed?

Assets are images, scripts, or other files that are incorporated into documentation and made publicly available to customers. The following locations are used to store these assets:

|Asset Type|Storage Type|Location|Rationale|
|---|---|---|---|
|Images (PNG, JPG)|Perforce repository|`[geo_proxy]:1111 //pubs/products/Cloud/smart-tools/images/`|Used as a backup location for images that are included in new or updated articles. This is updated every time a content backup is performed.|
|Source files for generating finished images (e.g., Powerpoint files, Visio files, etc.)|Perforce repository|`[geo_proxy]:1111 //pubs/products/Cloud/smart-tools/images/source`|Used by other authors or Localization so that updated or localized versions of the image can be created at a future date.|
|Downloadable files (PDF, script samples)|Adobe Experience Manager (AEM)|`/content/dam/docs/en-us/lifecycle-management/downloads`|Enables authors to version downloadable files without breaking customers' links to the original URL.|
|Content source files for Getting Started guides|ShareFile|CWC_CI folder at `https://citrixdesign.sharefile.com`|Since Product Design uses ShareFile to manage the design layouts for Smart Tools Getting Started guides, it makes sense to keep the content source here as well.|

### Access to Perforce

To use Perforce to store and version assets, you need a Perforce account and the P4V Client installed on your computer. To request an account and download the client software, see [Request access to Perforce](https://no-url.html).

For more information about using the P4V Client to manage files, see [Getting Started with P4V](https://www.perforce.com/perforce/doc.current/manuals/p4v-gs/01_p4v-gs.html) on the Perforce web site.

### Access to AEM

For access instructions, see [Getting Started with AEM to Author Product Documentation][https://no-url.html].

For more information about using AEM, refer to the [Citrix Product Documentation Home](https://no-url.html) Confluence page.

For specific questions about AEM that the links above don't cover, submit them to the `#ix-aem-community` Slack channel.
