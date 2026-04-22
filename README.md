#!/bin/bash

# Ask user for directory
echo "Enter the directory path to organize:"
read dir

# Check if directory exists
if [ ! -d "$dir" ]
then
    echo "Directory does not exist!"
    exit 1
fi

# Create folders
mkdir -p "$dir/Images"
mkdir -p "$dir/Videos"
mkdir -p "$dir/Documents"
mkdir -p "$dir/Music"
mkdir -p "$dir/Others"

# Counters
img_count=0
vid_count=0
doc_count=0
music_count=0
other_count=0

# Loop through files
for file in "$dir"/*
do
    if [ -f "$file" ]
    then
        # Extract extension
        ext="${file##*.}"
        # Convert extension to lowercase
        ext=$(echo "$ext" | tr 'A-Z' 'a-z')
        case "$ext" in
            jpg|jpeg|png|gif)
                mv "$file" "$dir/Images/"
                img_count=$((img_count + 1))
                ;;
            mp4|mkv|avi)
                mv "$file" "$dir/Videos/"
                vid_count=$((vid_count + 1))
                ;;
            pdf|doc|docx|txt)
                mv "$file" "$dir/Documents/"
                doc_count=$((doc_count + 1))
                ;;
            mp3|wav)
                mv "$file" "$dir/Music/"
                music_count=$((music_count + 1))
                ;;
            *)
                mv "$file" "$dir/Others/"
                other_count=$((other_count + 1))
                ;;
        esac
    fi
done

# Display summary
echo "-----------------------------"
echo "Files Organized Successfully!"
echo "Images: $img_count"
echo "Videos: $vid_count"
echo "Documents: $doc_count"
echo "Music: $music_count"
echo "Others: $other_count"
echo "-----------------------------"
