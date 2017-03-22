# financial-papers
The Drupal Feature module to replicate the George Washington Financial Papers project


Overview
What this module includes
  Content types
  Taxonomy vocabularies
  Views
Step 1. Installing and enabling modules
Step 2. Customizing the data model
Step 3. Organizing and customizing the default menu
Step 4. Automatic Nodetitles settings
Step 5. Enabling blocks
Step 6. Populating taxonomies
Step 7. Adding content
  One node at a time
  Using Editview
  Importing data
Step 8. Modifying displays
Step 9. Theming
Content type details
  Account
  Book
  Book page
  Double-entry line
  Person
  Place
  Ship
  Single-entry line
View details
  Account book pages
  Browsing
  Browsing (tax terms)
  Listed books
  Map
  Page overview
  References
  Search
  Taxonomy Description
  Taxonomy term
  Transcription lines


## Overview
The Financial Papers Drupal Feature module packages up the configuration used by the George Washington Financial Papers site to facilitate the development of other financial papers projects. Any project that is running Drupal 7 can install and enable the module to activate on their own site the data model created for the George Washington Financial Papers, as well as a number of the displays used for viewing, searching, and browsing the content on that site. While we anticipate that most projects will make some adjustments to the data model based on the particulars of their data and the interests of their audience, working from an existing model can significantly speed up the process of developing a new project. 

The Financial Papers Drupal Feature module uses a number of controlled vocabularies, some of which have a starter set of terms included along with the module (e.g. document type, transaction type), and some of which will need to be populated by the developers of other projects, based on their own data (e.g. names of source archives). 

Separate from the module, we have also posted on Github sets of terms that developers of other projects can optionally import as a starting point, such as currencies and occupations. Documentation accompanying the module describes, step-by-step, how developers can customize it to address the specific, unique needs of their own project.

## What this module includes
Enabling the Financial Papers module will add the following things to your Drupal site. While it is primarily intended as a way to jump-start development from a new Drupal site, almost all components have a machine name prefixed with *de*_ (documentary editing), meaning that they should not cause technical errors on your site even if you already have a content type, view, etc. with that same name.

### Content types
Content types are templates for storing different kinds of content. Content types can include 
- Account: used to capture documents like receipts or letters that aren’t a set of stand-alone lines, but contain financial information.
- Book: Used as a container for information about each ledger itself.
- Book page: A page in an account book.
- Double-entry line: A double-entry (i.e. with credit on one side and debit on the other) line on a book page
- Person: A person referenced in an account book, and/or the holder of an account.
- Place: A place referenced in an account book.
- Ship: A ship referenced in an account book
- Single-entry line: A single-entry line.

### Taxonomy vocabularies
Drupal’s taxonomy system is used to store controlled or uncontrolled (tagging) vocabularies. Some of these vocabularies have fields attached to their terms.
- Agriculture
  - Citation (text)
- Counties
- Countries
- Currencies
  - Name variations (text)
  - Notes (long text)
- Document/object type
- Events/occasions
  - Citation (text)
  - Canonical URL (link)
- Food and beverage
  - Citation (text)
- Occupations
  - Citation (text)
  - Services (term reference to Services)
- Place types
  - Citation (text)
- Services
  - Citation (text)
  - Services rendered by (term reference to Occupations)
- Sources
- State
- Transaction types

*Note*: the “Services” field in the “Occupations” vocabulary and the “Services rendered by” field in the “Services” vocabulary are reciprocal. If you plan to make use of this feature extensively, you may want to remove those existing term reference fields and replace them with [Corresponding Entity Reference](https://www.drupal.org/project/cer) fields.

### Views
Views are displays of your data, which can optionally be filtered and edited by users.
- Account book pages -- lists all pages of account book, displayed on Book node
- Browsing -- browsing interface for metadata facets that are based on a node reference field (places, people, ships). Includes a data export for people nodes.
- Browsing (tax terms) -- browsing interface for metadata facets that are based on a term reference field (occupation/title, services, food/beverage, agriculture, place type)
- Listed books -- a table of all account books
- Map -- a map visualization of the places in the database
- Page overview -- customized display of some components of a book page
- References -- displays account holders, people, places, and/or ships that are referenced in a node
- Search -- a more robust search page than the default, with numerous exposed options
- Taxonomy Description -- displays information about taxonomy terms (e.g. definitions, citations, broad/narrow terms)
- Taxonomy term -- overrides the default display that you get when clicking on a taxonomy term. Displays content tagged with a term, but limits it to “person”, “book”, “book page”, or “place”.
- Transcription lines -- displays the transcribed lines from a single-entry ledger and each side of a double-entry ledger. Includes a CSV and XLS data export for each ledger.

## Step 1. Installing and enabling modules
The Financial Papers feature module formally lists the following modules as dependencies. These modules must be installed before you can enable the Financial Papers feature, and they will automatically be enabled along with Financial Papers.
- [Display Suite](https://www.drupal.org/project/ds): used to create multi-column displays of content types
- [Chaos tool suite](https://www.drupal.org/project/ctools): required for Views and other modules
- [Date](https://www.drupal.org/project/date): provides a simple date field
- Date API: required by Date, part of the same module package
- [Entity](https://www.drupal.org/project/entity): required by Field Collection
- [Features](https://www.drupal.org/project/features): required to install Financial Papers and other modules that package up configuration as a module
- [Field Collection](https://www.drupal.org/project/field_collection): enables repeating groups of fields (in this case, currency and value)
- [Field Group](https://www.drupal.org/project/field_group): can group fields on content editing and display forms into tabs
- [Geofield](https://www.drupal.org/project/geofield): used to store geographic data
- [GeoPHP](https://www.drupal.org/project/geophp): required by Geofield
- [Leaflet](https://www.drupal.org/project/leaflet): mapping library; requires you to install the leaflet library in sites/all/libraries
- Leaflet Views: part of the Leaflet module package, allows you to create views that use the Leaflet display
- [Libraries](https://www.drupal.org/project/libraries): required by Leaflet
- [Link](https://www.drupal.org/project/link): provides a URL field
- Node Reference: provides a field for pointing to another node;part of References module package
- [Partial Date](https://github.com/agile-humanities/agile_partial_date): supports historical, approximate, and incomplete dates. Be sure to use the version on Github, linked here.
- [References](https://www.drupal.org/project/references): has module for pointing to users and nodes
- [Strongarm](https://www.drupal.org/project/strongarm): allows feature modules like Financial Papers to include content type settings like pathauto configurations, comment settings, etc.
- [Universally Unique Identifier](https://www.drupal.org/project/uuid): required by UUID Features
- [UUID Features](https://www.drupal.org/project/uuid_features): allows features modules like Financial Papers to export taxonomy terms
- [Views](https://www.drupal.org/project/views): used to generate displays of your data; essentially, an interface to generate database queries
- [Views Data Export](https://www.drupal.org/project/views_data_export): allows you to create a view for exporting your data as CSV, XLS, XML, etc.

The modules below are not formally required, but should be installed and enabled:
- [Automatic Nodetitles](https://www.drupal.org/project/auto_nodetitle): automatically populates the required “Drupal title” for a node using other metadata. (You may want to use [Automatic Entity Label](https://www.drupal.org/project/auto_entitylabel), which is less widely used but better supported, instead.)
- [Chosen](https://www.drupal.org/project/chosen): provides a select list with autocomplete-style features. Note that this requires you to install a library. 
- Display Suite UI: part of the Display Suite module package, allows you to edit Display Suite settings
- [Pathauto](https://www.drupal.org/project/pathauto): lets you specify patterns to improve the URLs of your nodes and taxonomy terms (by default, these look something like /node/123)
- [Taxonomy CSV](https://www.drupal.org/project/taxonomy_csv): provides simple CSV import/export of taxonomy terms. Will be used by George Washington Financial Papers in the future to disseminate vocabulary terms
- [Token](https://www.drupal.org/project/token): required by Pathauto
- [Token Tweaks](https://www.drupal.org/project/token_tweaks): having Entity enabled when you’ve enabled Token can lead to configuration pages crashing due to the token picker having to load too many tokens. Token tweaks puts a cap on the number of “levels” the token picker should load, making the configuration pages render faster.
- [Views Fieldsets](https://www.drupal.org/project/views_fieldsets): adds fieldsets to Views
- [Views Selective Exposed Filters](https://www.drupal.org/project/views_selective_filters): an exposed filter that automatically updates the options available based on your current result set
- Views UI: part of Views module package, lets you edit views

It will take Drupal some time to make all the necessary changes if you enable all these modules at once -- don’t be alarmed!

## Step 2. Customizing the data model
Look closely at the data model diagram below, and at the field descriptions for each of the content types. Does the data model capture everything you want to capture about your financial records? Are all the fields relevant to your financial records? Come up with a plan for how to adapt the data model to your own financial records: which fields to delete, and which fields to add, and make those changes before moving forward. (To learn more about data modeling for Drupal, read chapter 5 of *Drupal for Humanists*. Chapter 6 covers different field types, and chapter 7 applies data modeling to a specific example and describes how to add and edit content types.) 

Below is a diagram showing the content types (blue squares) and their connections to each other and to the taxonomies (yellow circles). The primary content in this data model -- the financial documents themselves -- are hierarchically structured, with a “Book” node at the top level, and “Book Page” nodes that point to their parent “Book”. The “Single-Entry Line”, “Double-Entry Line”, and “Account” content types store the financial information itself, and point to a parent “Book Page”. Typically, only one of these most granular content types (Single-Entry Line, Double-Entry Line, or Account) would be associated with a given page, but different pages in a book can be associated with different granular content types (e.g. a book may have pages that contain Single-Entry Lines, and other pages that contain Account lines, but it is unlikely that one page will contain both. There’s no technical barrier to it happening, but the display may look odd.

You may notice that some transaction metadata is being assigned at the “Book page” level rather than the “Single-entry line” or “Double-entry line” level, where other information about a transaction (e.g. credit or debit, currency, value, etc.) is being collected. From an idealized data modeling point of view, the transaction metadata “should” be part of the “Single-entry line” and “Double-entry line” content type. Developing and implementing a data model in practice, however, often requires making concessions to accommodate the reality of data entry. For the George Washington Financial Papers, it was more realistic to add transaction metadata at the page level, instead of more granularly at the line level, in order to save time. Enriching the line level with this metadata is one potential future area of expansion for that project.

The Financial Papers module uses this same approach, but it would not be difficult to change it to assign the metadata at the line level. Go to *Structure > Content types > Double-entry line (or Single-entry line) > Manage fields*. Towards the bottom of that page, look for “Add existing field” and add, one at a time, the following fields: 
- Ships
- Occupation/title
- Services
- Food and beverage
- Agriculture
- Events/occasions

If you take this approach, you may also want to assign values at the Single/Double-Entry Line level, rather than the Book Page level. These fields exist at both levels:
- Account name (data)
- People
- Places
- Currencies

At that point, if you haven’t added data to those fields at the page level, you can remove them from the “Book page” content type. (If you remove them from the “Book page” content type before you’ve added them elsewhere, they will be deleted completely from the system and you’ll have to re-add them as new fields.)

If you decide to store this metadata about transactions at the line level but still want to aggregate the information at the page level, you can create a view block of nodes from the single-entry line or double-entry line content types, add the field(s) you want to display, and add a contextual filter “Content: Book page”, set the default value to be “Content ID from URL”. Enable the block on the page content type, either using the Blocks configuration page (*Structure > Blocks or /admin/structure/block) or by adding the block as a custom field accessible to Display Suite in Structure > Display Suite > Fields > Add a block field* (/admin/structure/ds/fields/manage_block) and making it visible on the “Book page” content type’s “Manage display” page.


## Step 3. Organizing and customizing the default menu
Installing and enabling the Financial Papers module will add many pages to the main menu -- so many that it is likely to spill over onto a second like. Out of the box, the module can add these pages (all of which are generated using Views) to the main menu, but it’s more difficult to export their arrangement.

You may want to create a couple custom landing pages, and have those appear as top-level menu items, and set some of the browse-by pages to be sub-pages. For instance, on the *George Washington Financial Papers* site, there’s an [“Explore” page](http://financial.gwpapers.org/?q=explore) that was created as a 3-column panel node, consisting of custom blocks that each contain an image and a link to an individual browse-by page.

To edit the menu, go to *Structure > Menus > Main menu* (/admin/structure/menu/manage/main-menu). For any menu item that you don’t want to include in your menu at all, you can uncheck the “enabled” box; be sure to save your changes. To rearrange items, use the + sign to the left of the title to drag and drop the items into a different order. You can also use the + sign to drag an item beneath another, making it a sub-item. 

The default Drupal theme doesn’t display sub-items as drop-downs (or at all, in the case of the main menu), and it isn’t mobile-optimized, so you should plan to change it, as described below. When choosing a theme, you should look for one that has a menu region so you can take advantage of [drop-down menus](http://drupal.forhumanists.org/drupal-humanists-chapter-11-menus-and-blocks/dropdown-menus), if you set up some of the menu items as sub-items.

## Step 4. Automatic Nodetitles settings
Automatic Nodetitles (which automatically creates the required “Drupal title” for pages based on other metadata that you’ve already provided -- see *Drupal for Humanists* section 5.4.7 for more on “Drupal titles”) currently can’t export its settings via a Feature module, so you’ll need to set it up independently on your site. (Note: you may want to use [Automatic Entity Label](https://www.drupal.org/project/auto_entitylabel) instead; it works similarly, but has active maintainers, unlike Automatic Nodetitles which is widely used but officially no longer supported.)  While you can come up with your own patterns, some suggestions are listed below. Be sure to set these up before you start adding content to the site; while it’s possible to update the node titles later, it’s easier if you can be consistent from the start.

Go to the “edit” page for each of the following content types (*Structure > Content types > [Content type name])* or /admin/structure/types and click the “edit” link for each one. Under “Automatic title generation” (the first in a set of vertical tabs), select the radio button “Automatically generate the title and hide the title field”, and under “Pattern for the title”, enter the text below:
- Book page: [node:field_de_book]: pg. [node:field_de_page_number] [node:field_de_folio]
- Double-entry line: [node:field_de_book_page], [node:field_de_folio]: [node:field_de_line_number]
- Single-entry line: [node:field_de_book_page]: [node:field_de_line_number]

## Step 5. Enabling blocks
Enable the blocks listed below in the specified regions, by going to *Structure > Blocks* (admin/structure/block). Depending on your theme, the names for these regions may vary.
- Content / Main content:
  - View: Taxonomy description: Narrow terms
- Sidebar / Sidebar first or second:
  - View: References: Account name references **only for Account Names, Places**
  - View: References: People references 
  - View: References: Place references
  - View: References: Ship references

## Step 6. Populating taxonomies
Many of the content types have at least one “term reference field” (i.e. a field that allows you to select one or more terms from a vocabulary, typically a controlled vocabulary). Before you start adding content, you’ll first need to add some terms. 

The vast majority of term reference fields use the “select list” widget, which does not allow you to add new terms to the vocabulary as you add new content. (This widget, by itself, is ugly and makes it awkward to select more than one value; this is why the Chosen module is useful, since it replaces the default “select list” with an improved one with an autocomplete-like interface that is compatible with controlled vocabulary, in contrast to the out-of-the-box autocomplete widget.) If it makes more sense with your project for editors to add taxonomy terms as they add content, you can change the widget from “select list” to “autocomplete term widget (tagging)”.

To add new terms in advance, if you have the [Administration Menu](https://www.drupal.org/project/admin_menu) module installed, use the menu to go to *Structure > Taxonomy > [Taxonomy name] > Add term*.  

The following taxonomies already come with terms from the George Washington Papers project:
- Transaction types (credit, debit)
- Countries
- State

These taxonomies can optionally be imported:
- Currencies

These taxonomies may be included in a future version of the Financial Papers module, and/or may be made available as a CSV for import:

- Agriculture
- Food and beverage
- Occupations
- Place types
- Services

## Step 7. Adding content
There are a few ways to add content to your site, and you may use more than one method while building your site.

### One node at a time
You can add content one node at a time by going to *Content > Add content > [choose a content type]*. This is the easiest way to get started, particularly if you’re still a little unsure whether your data model is going to work for all your materials. (In theory, you want to resolve data model issues before you start adding content; in practice, adding content is a way to validate your data model, and it’s common to make some adjustments as you go.) If you have a multi-person team with varying levels of expertise, you can configure permissions (see section 10.5 of *Drupal for Humanists*) so that some team members only have permission to add particular content types, and not others, and/or only edit or delete nodes that they’ve created themselves.

### Using Editview
Instead of clicking through the menu to add each node, you can [use the Editview module](http://drupal.forhumanists.org/chapter-13-advanced-views/editview) to create a view that lets you add and edit multiple nodes from within a single page.

### Importing data
If your data already exists in some structured form (e.g. Excel, FileMaker, XML, etc.) that aligns with the data model on your Drupal site, you can use the Feeds module to import it in bulk. The easiest way to do this is using a CSV file (which you can export from Excel, FileMaker, Microsoft Access, and other software) as your source, but there are also modules that let you import from XML, as in [this TEI example](http://drupal.forhumanists.org/drupal-humanists-chapter-14-importing-data/importing-xml).

## Step 8. Modifying displays
All views described below under “View Details” can be edited to show more, less, or different information. You can also create new displays for those views, and/or entirely new views, depending on the needs of your project. The views that come with the Financial Papers feature module can serve a a model; for a more in-depth walkthrough of how the Views module works, consult chapters 12 and 13 in *Drupal for Humanists*.

In addition to the stand-alone views (like the various browsing pages and the search page), there are a number of Views-created blocks that are embedded in the display of the Book and Book Page content types, through the use of Display Suite block fields. Under “Source view”, the text before the colon indicates the view name, and the text after the colon indicates the display name:

| Block field name | Source view | Appears in content type |
| ---------------- | ----------- | ----------------------- |
| Book page list | Account book pages  |  |
| Credit transcription | Transcription lines: Double entry right | Book Page |
| Debit transcription | Transcription lines: Double entry left | Book Page |
| Image credit | Page overview: Credit image | Book Page |
| Listed book pages | Account book pages | Book |
| Page overview - information | Page overview: Information | Book Page |
| Single/debit image | Page overview: Single/Debit Image | Book Page |
| Single entry transcription | Transcription Lines: Single entry | Book Page |

## Step 9. Theming
Theming (choosing an existing Drupal theme that provides the “look and feel” for your site, or developing a custom theme) inevitably happens on a project-by-project basis, influenced by any existing branding and style guides used by the parent organization. The George Washington Financial Papers project uses a custom sub-theme of AdaptiveTheme, which provides the technical underpinnings that support features like mobile-responsiveness, which is a “must-have” for modern websites, and can be quite challenging to implement from scratch. There are a number of sub-themes for [AdaptiveTheme](https://www.drupal.org/project/adaptivetheme) that projects can use or build on, such as [Corolla](https://www.drupal.org/project/corolla), [Sky](https://www.drupal.org/project/sky), [AT Commerce](https://www.drupal.org/project/at_commerce), and [Pixture Reloaded](https://www.drupal.org/project/pixture_reloaded), but for a polished look, expect to do some CSS work. If you have AdaptiveTheme or one of its subthemes set as default, you can go to the settings area (*Appearance > Settings > [Theme/sub-theme name])*, and under the “Extensions” tab section, check the box for “Custom CSS”. When you save and the page reloads, a new “Custom CSS” tab will be available under the “Extensions” area where you can add custom CSS. One advantage of putting custom CSS in this area, rather than modifying the CSS files of the theme itself, is that you can update the theme without losing your CSS changes. For more on theming in general, and AdaptiveTheme in particular, consult chapter 18 of *Drupal for Humanists*.

## Content type details
The fields are often organized using a set of vertical tabs that appear along the left side when you edit each account name. Tab headers are given below in italics, where available. Additional system-level information (e.g. relating to the URL path settings) is not included.

### Account
Used to capture documents like receipts or letters that aren’t a set of stand-alone lines, but contain financial information.
- Book page (node reference to Book page node)
- Date (data) (partial date)
- Dateline (text)
- Salutation (text)
- Entry (long text)
- Entry regularized (long text)
- Closing (text)
- Signed (text)
- Endorsement (text)
- PS (text)
- Notes (text)
- Account name (data) (node reference to Person node)
- Place (node reference to Place node)

### Book
The Book content type is used as a container for information about each ledger itself.
- Book title (Drupal title field)
- Account owner (node reference to Person node)
- Accession number (text)
- Original source title (text)
- Source/Repository (term reference to Source vocabulary)
- Library of Congress Link (URL)
- Related accounts (node reference to Book node)
- Time period (term reference to Time Period vocabulary)
- Annotation (long text)
- Transcription available (boolean)
- Date Range (partial date and time range)

### Book page
The Book page content type is used to store information about an individual book page, as well as some metadata about the transactions that are recorded on that page (for ease of data entry).

Automatic Nodetitle pattern: [node:field_book]:, pg. [node:field_page_number] [node:field_folio]
- *General*
  - Book (node reference to Book node)
  - Citation name (text)
  - Page number (text)
  - Next page (node reference to Book page node)
  - Previous page (node reference to Book page node)
- *Images*
  - Page image (image; for single-entry ledgers)
  - Page image debit (image; left side image for double-entry ledgers)
  - Page image credit (image; right side image for double-entry ledgers)
- *Data*
  - Account name (data) (node reference to Person node)
  - People (node reference to Person node)
  - Places (node reference to Place node)
  - Ships (node reference to Ship node)
  - Occupation/Title (term reference to Occupation/Title vocabulary)
  - Services (term reference to Services vocabulary)
  - Food and Beverage (term reference to Food and Beverage vocabulary)
  - Agriculture (term reference to Agriculture vocabulary)
  - Currencies (term reference to Currencies vocabulary)
  - Events/Occasions (term reference to Events/Occasions vocabulary)
- *Annotation*
  - Annotation (long text)

### Double-entry line
A double-entry line has debit information on one side, and credit information on the other side.

Automatic Nodetitle pattern: [node:field_de_book_page], [node:field_de_folio]: [node:field_de_line_number]

- *General*
  - Book page (node reference to Book Page content type)
  - Book page line number (integer)
  - Folio (list; values: left, right)
  - Has Annotation (boolean)
  - Notes (long text)
  - Needs Formatting (boolean)
  - Needs Research (boolean)
- *Transcription*
  - Year (text)
  - Month (text)
  - Day (text)
  - Account name (transcription) (text)
  - Entry (long text)
  - Subtotal (text)
  - Page (text)
  - £ (boolean)
  - Pounds (text)
  - Shillings (text)
  - Pence (text)
  - Dollars (text)
  - Cents (text)
- *Data*
  - Date (partial date)
  - Debit/Credit (data) (term reference to Transaction Type vocabulary)
  - Account name (data) (node reference to Person node)
  - People (node reference to Person node)
  - Places (node reference to Place node)
  - Page (data) (text)
  - Entry regularized (long text)
  - Value and currency (field collection)
    - Pounds data (text)
    - Shillings data (text)
    - Pence data (text)
    - Dollars data (text)
    - Cents data (text)
    - Currency (term reference to Currency vocabulary)

### Person
The Person content type contains information about the person affiliated with each account that appears in the ledgers. Also used for people mentioned.

- *General information*
  - ID (text)
  - Name (node title)
  - Name variations (text)
  - Description (long text)
  - Birth (partial date)
  - Death (partial date)
  - Citation (text)
- *Details*
  - Gender (text list, m/f)
  - Occupation / Title (term reference)
  - Related places (node reference to Place nodes)
  - Related ships (node reference to Ship nodes)
  - Related people (node reference to Person nodes)

### Place
The Place content type is referenced from numerous other content types, and is used to generate a map visualization.
- *General information*
  - ID (text)
  - Place name (title)
  - Description (long text)
- *Details*
  - County (term reference to County vocabulary)
  - State (term reference to State vocabulary)
  - Country (term reference to Country vocabulary)
  - Geolocation (geofield, latitude and longitude)
  - Place type (term reference to Place Type vocabulary)
  - Related Places (node reference to Place node)
  - Related People (node reference to Person node)
  - Citation (text)

### Ship
A ship referenced in an account book.
- Ship name (title)
- Description (long text)
- Name variations (text)
- Notes (long text)
- Related people (node reference to Person node)
- Citation (text)

### Single-entry line
Automatic Nodetitle pattern: [node:field_book_page]: [node:field_book_page_line_number]
- *General*
  - Book page (node reference to Book Page node)
  - Line number (integer)
  - Notes (long text)
- *Transcription*
  - Year (text)
  - Month (text)
  - Day (text)
  - Account name (transcription) (text)
  - Entry (long text)
  - Subtotal (text)
  - £ (boolean)
  - Pounds (text)
  - Shillings (text)
  - Pence (text)
  - Dollars (text)
  - Cents (text)
- *Data*
  - Date (partial date)
  - Debit/credit (term reference to Transaction Type vocabulary)
  - Account name (data) (node reference to Person node)
  - People (node reference to Person node)
  - Place (node reference to Place node)
  - Entry regularized (long text)
  - Value and currency (field collection)
    - Pounds data (text)
    - Shillings data (text)
    - Pence data (text)
    - Dollars data (text)
    - Cents data (text)
    - Currency (term reference to Currency vocabulary)

## View details

### Account book pages
Provides a block display that is used for the “Listed book pages” custom block field, which appears on the Book content type display.
- Format: 2-column grid, displaying fields
- Fields: Title, Account name
- Filter: Content: Type = Book page
- Sort criteria: Content: Title (asc)
- Pager: Full pager, 20 items

### Browsing
Provides browsing pages for places, people, and ships, and a data export attached to the People page.

#### Places display (page)
- Format: Table
- Fields: Content: Title (Place name), Content: Country (Country), Content: State (State), Content: County (County), Content: Place type (Place type), Content: Path -- *exclude from display*, Content: Description (Description) -- *under Rewrite Results, check “Trim this field to a maximum length”, 200 characters, add ellipsis, add read-more link, More link text “Read More” and More link path [path]*
- Filter criteria: Content: Published (Yes), Content: Type = Place, Content: Title (exposed), County (selective, exposed), State (selective, exposed), Country (selective, exposed), Place type (selective, exposed)
- Sort: Title (asc)
- Path: /places
- Pager: Full pager, 50 items

#### People display (page)
- Format: Table
- Fields: Content: Title (Name), Content: Birth (Birth), Content: Death (Death), Field: Occupation/title (Occupation/title), Content: Path -- *exclude from display*, Content: Description (Description) -- *under Rewrite Results, check “Trim this field to a maximum length”, 200 characters, add ellipsis, add read-more link, More link text “Read More” and More link path [path]*
- Filter criteria: Content: Published (Yes), Content: Type = Person, Content: Title (exposed), Content: Birth:year (exposed), Content: Death:year (exposed), Content:Gender (exposed), Occupation/title (selective, exposed)
- Sort: Title (asc)
- Path: /people
- Pager: Full pager, 50 items

#### Ships display (page)
- Format: Table
- Fields: Content: Title (Ship name), Content: People (Related people), Content: Path -- *exclude from display*, Content: Description (Description) -- *under Rewrite Results, check “Trim this field to a maximum length”, 200 characters, add ellipsis, add read-more link, More link text “Read More” and More link path [path]*
- Filter criteria: Content: Published (Yes), Content: Type = Ship, Content: Title (exposed), Content: Description (exposed)
- Sort: Content: Title (asc)
- Path: /ships
- Pager: Full pager, 50 items

#### People CSV (data export)
- Format: CSV file
- Fields: Content: Title (Name), Content: Birth (Birth), Content: Death (Death), Content: Gender (Gender), Field: Occupation/title (Occupation/title), Content: Related places (Places), Content: People (Related people), Content: Related ships (Ships)
- Filter criteria: Published (Yes), Content: Type = Person
- Sort: Content: Title (asc)
- Path: /people-csv, Attach to: People
- Pager: Display all items

### Browsing (tax terms)
Drupal requires separate views for content (i.e. nodes) and terms. This view creates browsing pages for taxonomy terms, whereas the “Browsing” view creates them for nodes. The view has five pages, each with a unique path and title and a different value for the filter, but the settings are otherwise the same: Page - Occupation / Title (/occupation-title), Page - Services (/services), Page - Food/Beverage (food-beverages), Page - Agriculture (/agriculture), Page - Place Type (/place-types)
- Format: 4-column grid, of fields; grouping field: (Parent) Taxonomy term: Name
- Fields: (Parent) Taxonomy term: Name -- *this uses a relationship to a parent term, to get the name of that parent term*, Taxonomy term: Name
- Filter criteria: Taxonomy vocabulary: Machine name = [varies by page]
- Sort criteria: (Parent) Taxonomy term: Name (asc), Taxonomy term: Name (asc)
- Pager: Display all items

### Listed books
Creates a page displaying all documents (i.e. all nodes of the Book content type), grouped by account owner.
- Format: 4-column grid, grouping field: Content: Account owner
- Fields: Content: Title, Content: Account owner -- *exclude from display, under “Style settings”, check “Customize field HTML” and choose H3*
- Filter criteria: Content: Published (Yes), Content: Type = Book
- Sort criteria: Content: Account owner (asc), Content: Title (asc)
- Path: /documents
- Pager: Display all items

### Map
A map visualization of the places in the database, with an identical block and page display.
- Format: Leaflet Map, Data source: Content: Geolocation; Title field: Content: Title, Description Content: Content: Description.
- Fields: Content: Title, Content: Geolocation, Content: Description
- Filter criteria: Content: Published (Yes), Content: Type = Place, Content: Place type (exposed), Content: County (exposed), Content: State (exposed), Content: Country (exposed)
- Path (page display): /map
- Pager: Display all items
- On the Page display, under “exposed form”, Exposed form in block: Yes. *Note: the exposed filters exist in a block separate from the map block. To have the exposed filters available to the map block, you need to enable both blocks, and ideally position them close to one another*.

### Page overview
A modified display of some of the components of the book page content type, which are then displayed back on book page nodes. Includes four blocks that vary only in the fields displayed.
#### Common configuration 
- Format: Unformatted list
- Filter criteria: Published (Yes), Content: Type = Book page
- Sort criteria: Content: Post date (desc)
- Pager: Display all items
- Contextual filter: Content: Nid

#### Information (block)
- Fields: Content: Account name (data) (Account name), Content: People (People/Organizations), Content: Places (Places), Field: Occupation/Title (Occupation/title), Content: Ships (Ships), Field: Services (Services), Content: Food and Beverage (Food and beverage), Content: Agriculture (Agriculture)
#### Single/Debit Image (block)
- Content: Page image, Content: Page image debit
#### Credit Image (block)
- Content: Page image credit
#### Annotation (block)
- Content: Annotation

### References
Displays account holders, people, places, and/or ships that are referenced in a book page node. Contains four blocks, for People, Places, Account names, and Ships. All settings are the same except for the relationship that is applied to each field and the Content: Type filter.

#### Configuration
- Format: 3-column grid of fields 
- Fields: ([relationship]) Content: Title, ([relationship] Content: Account name (data)
- Filter criteria: ([relationship] Content: Type = Book page
- Pager: Full pager, 30 items
- Contextual filter: Content: Nid
- Relationships: *varies by display, options include Content: People - reverse, Content: Places - reverse, Content: Account name - reverse, or Content: Ships: reverse*

### Search
Includes two pages (Search and Advanced Search) and two data exports (Search CSV and Search XLS) that are attached to both Search and Advanced Search.

#### Search (page)
- Format: Table
- Fields: Content: Book page (Book page), Content: Date (Date), Content: Account name (data) (Account name), Content: Account name (transcription) (Account name transcription), Content: Entry (Entry), Content: Subtotal (Subtotal), Content: £ (£), Content: Pounds (Pounds), Content: Shillings (Shillings), Content: Pence (Pence), Content: Entry regularized (Entry regularized)
- Filter: Content: Published (Yes), Content: Type (Account, Double-entry line, Single-entry line), Search: Search terms (exposed), Account name (data) (selective, exposed)
- Sort criteria: Content: Book page (asc), Content: Folio (asc)
- Path: /search
- Header: Global: Text area (with basic explanatory text), Global: Result summary
- Pager: Full pager, 50 items

#### Advanced search (page)
- Format: Table
- Fields: Content: Book page (Book page), Content: Date (Date), Content: Account name (data) (Account name), Content: Account name (transcription) (Account name transcription), Content: Entry (Entry), Content: Subtotal (Subtotal), Content: £ (£), Content: Pounds (Pounds), Content: Shillings (Shillings), Content: Pence (Pence), Content: Entry regularized (Entry regularized)
- Filter: Content: Published (Yes), Content: Type (Account, Double-entry line, Single-entry line), Search: Search terms (exposed), Account name (data) (selective, exposed), Content: Date:day (grouped), Content: Date:month (grouped), Content: Date:year (exposed), Content: Entry (exposed), Content: Entry regularized (exposed)
- Sort criteria: Content: Book page (asc), Content: Folio (asc)
- Path: /advanced-search
- Header: Global: Result summary

#### Search CSV
- Format: CSV file
- Fields: Content: Book page (Book page), Content: Debit/credit (data) (Dr/Cr), Content: Folio (Folio), Content: Year (Year), Content: Month (Month), Content: Day (Day), Content: Account name (transcription) (Account name transcription), Content: Entry (Entry), Content: Subtotal (Subtotal), Content: £ (£), Content: Shillings (sh), Content: Pence (d), Content: Dollars ($), Content: Cents (¢), Content: Date (Date), Content: Account name (data) (Account name), Content: Value and currency (Value and currency), Content: Entry regularized (Entry regularized)
- Filter: Content: Published (Yes), Content: Type (Account, Double-entry line, Single-entry line), Search: Search terms (exposed), Account name (data) (selective, exposed)
- Sort criteria: Content: Book page (asc), Content: Folio (asc)
- Path: /search/export-csv
- Pager: Display all items

#### Search XLS
Same configuration as Search CSV, except:
- Format: XLS file
- Path: /search/export-xls

### Taxonomy Description
A page with information about taxonomy terms (e.g. definitions, citations, broad/narrow terms), and a block that’s embedded in the Taxonomy Term view.
- Format: Unformatted list of fields
- Fields: Taxonomy term: Term description (Description), Field: Occupation/title (Occupation/title), Field: Services (Services), Global: Fieldset (Citation) containing Field: Citation (Citation)
- Sort: Taxonomy term: Name (asc)
- Path: /taxonomy-description/% Note: *the % is a placeholder for the contextual filter value*
- Pager: Use specified number of items, 1
- Contextual filter: Taxonomy term: Term ID
- Relationships: Taxonomy term: Parent term

### Taxonomy term
Overrides the default display that you get when clicking on a taxonomy term. Displays content tagged with a term, but limits it to “person”, “book”, “book page”, or “place”.
- Format: 3-column grid of fields
- Fields: Content: Path -- *exclude from display, Content: Description (Description) -- under Rewrite Results, check “Trim this field to a maximum length”, 200 characters, add ellipsis, add read-more link, More link text “Read More” and More link path [path]*, Content: Title, Content: Type
- Filter: Content: Published; Content: Type = Book, Book page, Person, Place; Content: Book (exposed)
- Sort: Content: Book (asc), Content: Page number (asc), Content: Title (asc)
- Path: /taxonomy/term/%
- Header: Global: View area (insert block from taxonomy description view)
- Pager: Full pager, 100 items
- Contextual filter: Content: Has taxonomy term ID (with depth), Content: Has taxonomy term ID depth modifier 

### Transcription lines
Three blocks that display the transcribed lines from a single-entry ledger and each side of a double-entry ledger. Includes a CSV and XLS data export for each ledger.

#### Blocks (Double entry left, Double entry right, Single entry)
- Format: Table
- Fields: Content: Book page (Book page), Content: Line number (Line number), Content: Has annotation (Has annotation), Content: Year (Year), Content: Month (Month), Content: Day (Day), Content: Account name (transcription) (Account name), Content: Entry (Entry), Content: Subtotal (Subtotal), Content: £ (£), Content: Pounds (£), Content: Shillings (sh), Content: Pence (d), Content: Dollars ($), Content: Cents (¢), Content: Delete link, Content: Edit link
- Filter criteria: Content: Published (Yes), Content: Type = *varies: Single-entry line, Double-entry line; For double entry variants:* Content: Folio = *Left or Right*
- Sort criteria: Line number (asc)
- Pager: Display all items
- Contextual filter: Content: Book page (provide default value: Content ID from URL)

#### Data export (Ledger CSV export, Ledger XLS export)
- Format: CSV file
- Fields: Content: Book page (Book page), Content: Line number (Line number), Content: Has annotation (Has annotation), Content: Year (Year), Content: Month (Month), Content: Day (Day), Content: Account name (transcription) (Account name), Content: Entry (Entry), Content: Subtotal (Subtotal), Content: £ (£), Content: Pounds (£), Content: Shillings (sh), Content: Pence (d), Content: Dollars ($), Content: Cents (¢), Content: Debit/credit (data) (Dr/Cr), Content: Folio (Folio side), Content: Account name (data) (Account name (data)), Content: Date (Date), Content: Value and currency (Value and currency)
- Path: /ledger-csv-export or /ledger-xls-export
- Pager: Display all items
- Contextual filter: Content: Book page (Default value: Content ID from URL)




