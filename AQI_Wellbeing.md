# Preparing Data:
1. Maintain a separate folder for each day. (E.g. Day 1, Day 2 ..)
2. Unique link for each user for each interval in a day should be generated Qualtrics -> Distributions -> Personal Links.
	i) Create a list of users (Each day 3 CSVs). 
	   Note: Save Phone No in Col Last Name (Unable to add new column, right now the script has Phone No saved in Last Name column)
	ii) Shuffle the sequence of recipients randomly each day.
	iii)Expiration time for link 2 hours after sending.

# Required Environment to Execute Scripts:
1. Install python, anaconda. (https://docs.anaconda.com/anaconda/install/)
2. conda create -n Env_Name
   conda activate Env_Name
   conda install pip 
   pip install jupyter notebook
   conda install jupyter notebook (first use, if not then go for pip)
3. pip install Flask pandas twilio werkzeug

# Random SMS Sending through Twilio
1. Set the parameter "total_time_slot" in config.ini as per the required time for processing 1 CSV. (Currently 4 hours (14400) seconds).
   The next CSV from same folder gets loaded after 4 hours.
2. Run the python file Random_AQI.py in same Env_Name.
3. Run http://127.0.0.1:5000 on browser, a UI will be opened.
4. Choose files -> Select a folder containing CSVs for that particular day.
5. The script sends SMS via twilio in 3 slots of 4 hours (If folder is uploaded at 8 a.m. then 8-12, 12-4 and 4-8)

# SMS Sending when Peak AQI Reading through Twilio
1. Set the parameter "total_time_slot1", "total_time_slot2" and "total_time_slot3" as per the required time for processing 
   each CSV and "sleep_time1" and "sleep_time2" as wait intervals. 
   The next CSV from same folder gets loaded after "total_time_slot"+"sleep_time" hours.
		For example If Peak AQI time is 11-12, 2-3:30, 5-6:15, 
		i)  start script at 11 am, set "total_time_slot1" for 1 hour (3600) seconds and "sleep_time1" as 2 hours (7200) seconds.
		ii) set "total_time_slot2" for 1:30 hour (5400) seconds and "sleep_time2" as 1:30 hour (5400) seconds.
		iii)set "total_time_slot3" for 1:15, hour (4500) seconds. (No sleep time as this is the last CSV file.)
2. Run the python file PeakTime_AQI.py in same Env_Name.
3. Run http://127.0.0.1:5000 on browser, a UI will be opened.
4. Choose files -> Select a folder containing CSVs for that particular day.
5. The script sends SMS via twilio in 3 slots of 1 hours, 1:30 and 1:15  (11-12, 2-3:30, 5-6:15) 
   with sleep_time1 and sleep_time2 set after each CSV completion.
	