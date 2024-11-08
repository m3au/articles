# Prettier Configuration

![prettierrc logo](prettierrc.png '# Prettier logo with .prettierrc text overlayed' =250x)

🔍 Overview of Prettier - Prettier is a code formatter tool that automatically formats your code according to a predefined set of rules and styles. It supports various programming languages like JavaScript, TypeScript, CSS, HTML, and more, ensuring consistent code formatting across your project. source

🛠️ Code Consistency - Prettier helps maintain a consistent coding style within your project by enforcing a uniform format for code indentation, line breaks, spacing, and other stylistic elements. This consistency improves code readability, collaboration, and reduces the time spent on manual formatting. source

🚀 Productivity Boost - By automating code formatting, Prettier streamlines the development process and allows developers to focus on writing code rather than worrying about formatting conventions. It eliminates debates over coding styles and ensures that the codebase adheres to a standardized format, enhancing productivity and code quality.

---

## Example from Playwright repository

This is the configuration file for Prettier. It is used to define the rules for formatting the code.

This file needs to be in the root directory of the project.

```json
{
  "arrowParens": "always", // Include parentheses around a sole arrow function parameter
  "bracketSpacing": true, // Print spaces between brackets in object literals
  "endOfLine": "lf", // Use Unix-style line endings
  "printWidth": 140, // Specify the line length that the printer will wrap on
  "semi": false, // Do not print semicolons at the ends of statements
  "singleQuote": true, // Use single quotes instead of double quotes
  "tabWidth": 2, // Specify the number of spaces per indentation-level
  "trailingComma": "all", // Print trailing commas wherever possible
  "useTabs": false // Indent lines with spaces, not tabs
}
```

---

Click here if you would like to know more

[Prettier Official website](https://prettier.io/).

![know more meme](know_more.png '# Starship troopers would you like to know more meme' =300x)
