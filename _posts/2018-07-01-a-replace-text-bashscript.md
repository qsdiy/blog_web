---
title: replace text scripts
tags: shell
---



---

一个用来处理文件夹内文本内容的简单脚本。

```
#!/bin/bash

# Function to replace text in Markdown files
replace_text() {
    local folder_path="/Users/tly/Documents/blog/blog/_posts/"
    local old_text="$1"
    local new_text="$2"
    local files_processed=0
    local replacements=0

    # Printing the values of $1, $2, and $3
    echo "Folder Path: $folder_path"
    echo "Old Text: $old_text"
    echo "New Text: $new_text"

    # Check if the directory exists
    if [ -d "$folder_path" ]; then
        # Iterate through all Markdown files in the folder
        for file in "$folder_path"/*.markdown; do
            if [ -f "$file" ]; then
                # Count the number of files processed
                ((files_processed++))

                # Perform the text replacement using sed and create a backup
                if sed -i '' -e "s/$old_text/$new_text/g" "$file"; then
                    ((replacements++))
                    echo "Replaced '$old_text' with '$new_text' in $file"
                else
                    echo "No replacements made in $file"
                fi
            fi
        done

        echo "Total Markdown files processed: $files_processed"
        echo "Total replacements made: $replacements"
    else
        echo "Directory '$folder_path' does not exist."
    fi
}

# Replace specified text in Markdown files
# Replace "old_text" with your desired text to replace
# Replace "new_text" with your desired new text

```



---


