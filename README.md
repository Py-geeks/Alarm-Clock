# Alarm System<br>
### Description
Its a handy alarm system made using python. 

### Tools and Languages:
<img align="left" alt="Python" width="26px" src="python.png" />
<img align="left" alt="pip" width="26px" height="34px" src="pip.png" />
<img align="left" alt="VS Code" width="26px" src="vscode.png" />
<br>

### Installing Libraries
```cmd
pip install datetime
pip install os
pip install time
pip install random
pip install webbrowser
```
-> Mostly probably you should already have OS. datetime, time and random libraries installed as it comes with python distribution.

### Steps to follow
-Install the given libraries<br>
-Download the code from the given github repository<br>
-Save your desired video link in file
-Run the code<br>

### Breaking the code
```python
if not os.path.isfile("youtube_alarm_videos.txt"):
    print('Creating "youtube_alarm_videos.txt"...')
    with open("youtube_alarm_videos.txt", "w") as alarm_file:
        alarm_file.write("https://youtu.be/xaXLLF2qm20")
```
In this conditional block, the code searches for the youtube_alarm_video.txt file. If there is no such file, it creates one. Then it writes the link of your desired video into the file.

```python
def check_alarm_input(alarm_time):
    if len(alarm_time) == 1: 
        if alarm_time[0] < 24 and alarm_time[0] >= 0:
            return True
    if len(alarm_time) == 2:
        if alarm_time[0] < 24 and alarm_time[0] >= 0 and \
           alarm_time[1] < 60 and alarm_time[1] >= 0:
            return True
    elif len(alarm_time) == 3: 
        if alarm_time[0] < 24 and alarm_time[0] >= 0 and \
           alarm_time[1] < 60 and alarm_time[1] >= 0 and \
           alarm_time[2] < 60 and alarm_time[2] >= 0:
            return True
    return False
```
This function checkes whether the user entered a valid time, otherwise it returns false.

```python
print("Set a time for the alarm (Ex. 06:30 or 18:30:00)")
while True:
    alarm_input = input(">> ")
    try:
        alarm_time = [int(n) for n in alarm_input.split(":")]
        if check_alarm_input(alarm_time):
            break
        else:
            raise ValueError
    except ValueError:
        print("ERROR: Enter time in HH:MM or HH:MM:SS format")
```
This block here takes input of time and checks for its validity.

```python
seconds_hms = [3600, 60, 1] 
alarm_seconds = sum([a*b for a,b in zip(seconds_hms[:len(alarm_time)], alarm_time)])
now = datetime.datetime.now()
current_time_seconds = sum([a*b for a,b in zip(seconds_hms, [now.hour, now.minute, now.second])])
time_diff_seconds = alarm_seconds - current_time_seconds
if time_diff_seconds < 0:
    time_diff_seconds += 86400 
print("Alarm set to go off in %s" % datetime.timedelta(seconds=time_diff_seconds))
time.sleep(time_diff_seconds)
print("Wake Up!")
with open("youtube_alarm_videos.txt", "r") as alarm_file:
    videos = alarm_file.readlines()
webbrowser.open(random.choice(videos))
```
Once the time is verified to be proper, the timer is set. When the timer goes off the video saved earlier is played in the browser window. 

### Developed by:
<a href="https://github.com/ankush0939">Ankush Mishra</a>

