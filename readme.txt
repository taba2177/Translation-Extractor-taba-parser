ParseBlade: Laravel Blade Translation Extractor
Overview
ParseBlade is a Laravel console command that simplifies localization by scanning Blade templates, extracting translatable strings, and organizing them into translation files. It works by identifying static text in Blade files, replacing it with translation directives, and saving the extracted strings into language files for easy localization.

Features
✨ Automatic Translation Extraction
Scan Blade templates within resources/views/ directory.
Extracts translatable content while skipping unwanted tags like <script>, <style>, and <meta>.
Generates translation keys for each translatable string, organized by HTML tags.
🔄 Translation Directive Replacement
Replaces static text with Laravel's translation directives:
{!! __('file.tag.key') !!} for content.
{{ __('file.tag_attribute.key') }} for attributes like content and onclick.
💾 Seamless Integration
Updates Blade templates with translation directives.
Generates or updates translation files in the resources/lang/en/ directory.
Installation
To integrate ParseBlade into your Laravel project:

Clone or add the code to your app/Console/Commands folder.
Run the command in your terminal to start the extraction process:
bash
Copy code
php artisan app:parse
Command Execution (php artisan app:parse)
Steps:
Load Blade Files:

Scans all Blade files in the resources/views/ directory to gather all templates.
Process Blade Files:

Extracts the filename and loads any existing translations.
Processes the Blade content to identify and replace translatable text with directives.
Save Updates:

Modified Blade files are saved back with translation directives.
The translation file is generated or updated in resources/lang/en/<filename>.php.
Detailed Functionality
Text Extraction and Replacement
processBladeContent
Handle Special Tags:
Uses regular expressions to identify and skip content inside <script>, <style>, and <meta> tags.
Extract Translatable Text:
Passes non-script content to the extractTranslations method for extraction and replacement.
extractTranslations
HTML Parsing with DOM:

Uses DOMDocument and DOMXPath to parse the HTML content.
Skips content inside Blade directives, whitespace, and dynamically generated text.
Key Generation:

Generates a unique translation key for each translatable text using the generateKey method.
processAttributeNode
Attribute Replacement:
Handles attribute values (e.g., content="value") and replaces them with translation directives like:
php
Copy code
{{ __('file.tag_attribute.key') }}
generateKey
Generate Unique Translation Keys:
Extracts the first significant words from the text.
Converts it to a slug format (e.g., Hello World becomes hello_world).
Save Translations
Output Structure:
The translations are written into PHP arrays:
php
Copy code
return [
    'div' => [
        'unique_key' => 'Hello',
    ],
    'meta_content' => [
        'description' => 'Sample meta description',
    ],
];
What It Does & Doesn't Do
✅ Does
Extracts static translatable text from Blade templates.
Supports UTF-8 encoded languages (e.g., Arabic).
Replaces text in HTML tags and attributes.
Skips Blade directives and dynamic content.
❌ Doesn't
Doesn't modify content inside <script>, <style>, or <meta> tags.
Doesn't process text that is already wrapped in Blade translation directives.
Practical Use Case
Localization Automation
ParseBlade automates the extraction of translatable strings for multilingual Laravel projects.
Keeps Blade templates clean, replacing static text with translation directives, while ensuring translatable content is centralized in language files.
Localization Management
Simplifies localization by centralizing all translatable strings into structured language files, making translation processes easier to manage.
Example Usage
To run the ParseBlade command:

bash
Copy code
php artisan app:parse
This will:

Process all Blade files in your resources/views/ directory.
Replace static text with translation directives.
Generate or update translation files in the resources/lang/en/ directory.
License
This project is licensed under the MIT License - see the LICENSE file for details.