#Section A

# Author: [Lambert] [Fru]
# Student ID: [011711777]

#Section B

# Switch statement to prompt user for actions
$continue = $true
while ($continue) {
    Clear-Host
    Write-Host "Select an action:"
    Write-Host "1. List .log files"
    Write-Host "2. List all files in alphabetical order"
    Write-Host "3. Display CPU and memory usage"
    Write-Host "4. List running processes by virtual size"
    Write-Host "5. Exit"

    $choice = Read-Host "Enter your choice (1-5)"

    switch ($choice) {
        1 {
            # Task B1: List .log files

            # Get the current date and format it
            $currentDate = Get-Date -Format "yyyy-MM-dd"

            # Define the path for the log file
            $logFilePath = "/Users/a/Downloads/Requirements1/DailyLog.txt"
            # Check if the log file already exists
            if (-not (Test-Path $logFilePath)) {
                # If it doesn't exist, create a new log file
                New-Item -ItemType File -Path $logFilePath -Force | Out-Null
            }
            # List all .log files and append the results to the log file
            Get-ChildItem -Filter *.log | Out-File -Append -FilePath $logFilePath
            # Add a separator for clarity
            Add-Content -Path $logFilePath -Value ("=" * 50)

        }
        2 {
            # Task B2: List all files in alphabetical order
            # Define the folder path
            $folderPath = "/Users/a/Downloads/Requirements1/"

            # List files in tabular format, sorted alphabetically, and redirect output to C916contents.txt
            Get-ChildItem -Path $folderPath | Sort-Object -Property Name | Format-Table -AutoSize | Out-File -FilePath "$folderPath\C916contents.txt"

        }
        3 {
            # Task B3: Display CPU and memory usage
            # Get CPU usage
            $cpuUsage = (Get-Counter '\Processor(_Total)\% Processor Time').CounterSamples.CookedValue

            # Get memory usage
            $memoryUsage = (Get-Counter '\Memory\% Committed Bytes In Use').CounterSamples.CookedValue

            # Display CPU and memory usage
            Write-Host "Current CPU Usage: $cpuUsage %"
            Write-Host "Current Memory Usage: $memoryUsage %"

        4 {
            # Task B4: List running processes by virtual size
            # Get all running processes and sort them by virtual size
            $processes = Get-Process | Sort-Object -Property WS

            # Display the sorted processes in grid format
            $processes | Format-Table -AutoSize

        }
        5 {
            # Task B5: Exit the script
            $continue = $false
        }
        default {
            Write-Host "Invalid choice. Please select a number from 1 to 5."
        }
    }
}

