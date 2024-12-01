# ParseBlade: Laravel Blade Translation Extractor

ParseBlade is a powerful Laravel console command that streamlines the localization process by scanning Blade templates, extracting translatable strings, and organizing them into translation files. It automates the replacement of static text with Laravel’s translation directives, ensuring your app is ready for multilingual support.

---

## ✨ Features

### 🔍 Automatic Translation Extraction

- Scans Blade templates in the `resources/views/` directory.
- Identifies and extracts translatable content.
- Skips non-translatable tags like `<script>`, `<style>`, and `<meta>`.

### 🛠️ Translation Directive Replacement

- Replaces static text with Laravel’s translation directives:
  - `{!! __('file.tag.key') !!}` for inline content.
  - `{{ __('file.tag_attribute.key') }}` for attributes like `title` or `content`.

### 📁 Language File Management

- Creates or updates translation files in `resources/lang/en/`.
- Organizes translatable content by HTML tag for better readability.

---

## 🚀 Installation

To use ParseBlade in your Laravel project:

1. Clone or copy the command file into the `app/Console/Commands/` directory of your Laravel project.
2. Register the command in your application (if needed).
3. Run the command in the terminal to start extracting translations:
   ```bash
   php artisan app:parse
   ```

## 🛠️ How It Works

- Step 1: Scanning Files
The command scans all Blade templates in the resources/views/ directory.

- Step 2: Extracting Translations
It parses Blade files, extracting static text while skipping:

Content inside <script>, <style>, and <meta> tags.
Blade directives and dynamic content.
Step 3: Saving Changes
Updates Blade templates by replacing static text with translation directives.
Writes extracted strings into organized translation files in resources/lang/en/.
## 🔄 Detailed Process
- Text Extraction and Replacement
- processBladeContent

Parses the Blade template content.
Skips unwanted tags and extracts translatable text.
extractTranslations

Uses DOMDocument and DOMXPath to identify text nodes.
Replaces static text with directives like {!! **('file.tag.key') !!}.
Handling Attributes
processAttributeNode
Handles attributes (e.g., title, content) by replacing their values with directives:
php
Copy code
{{ **('file.tag_attribute.key') }}
Generating Translation Keys
generateKey
Creates unique keys based on the text content.
Example: "Welcome to my site" → welcome_to_my_site.
## 📝 Example
Before
html
Copy code

<div>Welcome to our site!</div>
<meta name="author" content="Your Name">
## After
html
Copy code
<div>{!! __('file.div.welcome_to_our_site') !!}</div>
<meta name="author" content="{{ __('file.meta_content.author') }}">
Generated Language File
resources/lang/en/file.php:

php
Copy code
return [
'div' => [
'welcome_to_our_site' => 'Welcome to our site!',
],
'meta_content' => [
'author' => 'Your Name',
],
];
## ✅ What It Covers
Does:
Extract static text for localization.
Handle UTF-8 content (e.g., Arabic, Chinese).
Replace content inside text nodes and attributes.
Doesn’t:
Modify <script>, <style>, or <meta> tags.
Process content already wrapped in translation directives.
## 🏆 Practical Benefits
Automates Localization
Streamlines the localization process by automating string extraction and organizing translations into structured files.

Clean Code
Keeps your Blade templates clean and readable by replacing static text with standardized translation directives.

## ⚡ Usage
Run the command to process all Blade files:

bash
Copy code
php artisan app:parse
This will:

Extract all translatable strings from Blade templates.
Replace static text with translation directives.
Generate or update language files in the resources/lang/ directory.
📜 License
ParseBlade is open-source and licensed under the MIT License. You are free to use and modify it to suit your project needs.
