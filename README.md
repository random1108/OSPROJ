echo "Enter the directory path to organize:"
read dir

if [ ! -d "$dir" ]
then
    echo "Directory does not exist!"
    exit 1
fi

mkdir -p "$dir/Images"
mkdir -p "$dir/Videos"
mkdir -p "$dir/Documents"
mkdir -p "$dir/Music"
mkdir -p "$dir/Others"

imgc=0
vidc=0
docc=0
musc=0
otrc=0

# Loop
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
                imgc=$((img_count + 1))
                ;;
            mp4|mkv|avi)
                mv "$file" "$dir/Videos/"
                vidc=$((vid_count + 1))
                ;;
            pdf|doc|docx|txt)
                mv "$file" "$dir/Documents/"
                docc=$((doc_count + 1))
                ;;
            mp3|wav)
                mv "$file" "$dir/Music/"
                musc=$((music_count + 1))
                ;;
            *)
                mv "$file" "$dir/Others/"
                othc=$((other_count + 1))
                ;;
        esac
    fi
done

echo "-----------------------------"
echo "Files Organized Successfully!"
echo "Images: $imgc"
echo "Videos: $vidc"
echo "Documents: $docc"
echo "Music: $musc"
echo "Others: $othc"
echo "-----------------------------"
