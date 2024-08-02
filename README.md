# Bash Script Instructions

## Overview

This script allows you to select one of four `ffmpeg` commands to execute and then prompts you for the required arguments based on your choice.

## Usage

1. **Download the Script**

    Save the script below as `ffmpeg_script.sh`.

    ```bash
    #!/bin/bash

    # Function to display menu and get user choice
    function show_menu {
        echo "Select a command to execute:"
        echo "1) Concatenate: ffmpeg -f concat -i <input_file> -c copy <output_file>"
        echo "2) Extract Sound: ffmpeg -i <input_file> -q:a 0 -map a <output_file>"
        echo "3) Combine Sound: ffmpeg -i <input_file1> -i <input_file2> -c copy -map 0:v:0 -map 1:a:0 <output_file>"
        echo "4) Trim: ffmpeg -ss <start_time> -to <end_time> -i <input_file> -c copy <output_file>"
        read -p "Enter choice [1-4]: " choice
    }

    show_menu

    # Execute the selected command
    case $choice in
        1)
            read -p "Enter input file: " INPUT_FILE
            read -p "Enter output file: " OUTPUT_FILE
            echo "Concatenating files..."
            ffmpeg -f concat -i "$INPUT_FILE" -c copy "$OUTPUT_FILE"
            ;;
        2)
            read -p "Enter input file: " INPUT_FILE
            read -p "Enter output file: " OUTPUT_FILE
            echo "Extracting sound from video..."
            ffmpeg -i "$INPUT_FILE" -q:a 0 -map a "$OUTPUT_FILE"
            ;;
        3)
            read -p "Enter first input file: " INPUT_FILE1
            read -p "Enter second input file: " INPUT_FILE2
            read -p "Enter output file: " OUTPUT_FILE
            echo "Combining video and sound..."
            ffmpeg -i "$INPUT_FILE1" -i "$INPUT_FILE2" -c copy -map 0:v:0 -map 1:a:0 "$OUTPUT_FILE"
            ;;
        4)
            read -p "Enter start time: " START_TIME
            read -p "Enter end time: " END_TIME
            read -p "Enter input file: " INPUT_FILE
            read -p "Enter output file: " OUTPUT_FILE
            echo "Trimming video..."
            ffmpeg -ss "$START_TIME" -to "$END_TIME" -i "$INPUT_FILE" -c copy "$OUTPUT_FILE"
            ;;
        *)
            echo "Invalid choice."
            exit 1
            ;;
    esac

    echo "Command executed successfully."
    ```

2. **Make the Script Executable**

    ```bash
    chmod +x ffmpeg_script.sh
    ```

3. **Move the Script to a Directory in Your PATH**

    Option 1: Move to `~/bin` (for user-specific access)

    ```bash
    mkdir -p ~/bin
    mv ffmpeg_script.sh ~/bin/
    chmod +x ~/bin/ffmpeg_script.sh
    echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    ```

    Option 2: Move to `/usr/local/bin` (for system-wide access)

    ```bash
    sudo mv ffmpeg_script.sh /usr/local/bin/
    sudo chmod +x /usr/local/bin/ffmpeg_script.sh
    ```

4. **Run the Script**

    From any directory, run the script and follow the prompts:

    ```bash
    ffmpeg_script.sh
    ```

    You will be asked to select a command and then provide the necessary arguments. The script will then execute the chosen `ffmpeg` command with the provided arguments.
