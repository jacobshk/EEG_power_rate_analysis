Notes:
the full .zip file expands to the “ds005505” folder, with the following structure:

… (~400 “sub-” folders)

the dataset_description.json has some general info about the dataset
participants.json contains a schema for participants.tsv. column names:
participant_id  release_number  sex age ehq_total   commercial_use  full_pheno  p_factor    attention   internalizing   externalizing   RestingState    DespicableMe    FunwithFractals ThePresent  DiaryOfAWimpyKid    contrastChangeDetection_1   contrastChangeDetection_2   contrastChangeDetection_3   surroundSupp_1  surroundSupp_2  seqLearning6target  seqLearning8target  symbolSearch

{
 "participant_id": {
   "Description": "The prticipant ID set in the HBN dataset"
 },
 "release_number": {
   "Description": "The release in which the dataset was made available via the HBN project"
 },
 "sex": {
   "LongName": "Gender",
   "Description": "Gender",
   "Levels": {
     "F": "Female",
     "M": "Male"
   }
 },
 "age": {
   "LongName": "Age",
   "Description": "Age in years"
 },
 "ehq_total": {
   "LongName": "Handedness",
   "Description": "Edinburgh Handedness Questionnaire, +100=Fully Right-handed, -100=Fully Left-handed"
 },
 "commercial_use": {
   "Description": "Did the participant consent to commercial use of data?",
   "Levels": {
     "Yes": "Subject gave consent to commercial use of data",
     "No": "Subject did not give consent to commercial use of data"
   }
 },
 "full_pheno": {
   "Description": "Does the participant have a full phenotypic file?"
 },
 "p_factor": {
   "Description": "Single latent score indicatve of comorbid features of psychiatric disorders"
 },
 "attention": {
   "Description": "Focuses on attentional capacities or deficits, crucial in conditions like ADHD, affecting focus and concentration."
 },
 "internalizing": {
   "Description": "An indicator of inwardly directed psychological symptoms, typically involving mood and anxiety disorders."
 },
 "externalizing": {
   "Description": "Encompasses outwardly directed behavioral problems, often seen in disorders like ADHD and conduct disorder."
 },
 "RestingState": {
   "Description": "Availability status of the resting state task"
 },
 "DespicableMe": {
   "Description": "Availability status of watching the Despicable Me"
 },
 "FunwithFractals": {
   "Description": "Availability status of watching the Fun with Fractals"
 },
 "ThePresent": {
   "Description": "Availability status of watching the The Present"
 },
 "DiaryOfAWimpyKid": {
   "Description": "Availability status of watching the Diary Of A Wimpy Kid"
 },
 "contrastChangeDetection_1": {
   "Description": "Availability status of the 1st run of the contrast change task"
 },
 "contrastChangeDetection_2": {
   "Description": "Availability status of the 2nd run of the contrast change task"
 },
 "contrastChangeDetection_3": {
   "Description": "Availability status of the 3rd run of the contrast change task"
 },
 "surroundSupp_1": {
   "Description": "Availability status of the 1st run of the surround suppression task"
 },
 "surroundSupp_2": {
   "Description": "Availability status of the 2nd run of the surround suppression task"
 },
 "seqLearning": {
   "Description": "Availability status of the sequence learning task"
 },
 "symbolSearch": {
   "Description": "Availability status of the symbol search task"
 }
}

There are 9 unique tasks: we only care about seq learning 6 and 8 (right @Ted ?)  (note the README mentions 6 unique task types)

task name
from project readme
Despicable Me
3. **Movie Watching**: Participants watched four short movies with different themes, with event markers recording the start and stop times of presentations.


Contrast Change Detection
4. **Contrast Change Detection**: Participants identified flickering disks with dominant contrast changes and received feedback based on their responses.
Diary of a Wimpy Kid
3. **Movie Watching**: Participants watched four short movies with different themes, with event markers recording the start and stop times of presentations.


fun with fractals
3. **Movie Watching**: Participants watched four short movies with different themes, with event markers recording the start and stop times of presentations.
resting state
1. **Resting State**: Participants rested with their heads on a chin rest, following instructions to open or close their eyes and fixate on a central cross.
seq learning 6 target
5. **Sequence Learning**: Participants memorized and repeated sequences of flashed circles on the screen, designed for different age groups.
seq learning 8 target
5. **Sequence Learning**: Participants memorized and repeated sequences of flashed circles on the screen, designed for different age groups.
surround supp 
2. **Surround Suppression**: Participants viewed flashing peripheral disks with contrasting backgrounds, while event markers and conditions were recorded.
symbol search 
6. **Symbol Search**: Participants performed a computerized symbol search task, identifying target symbols from rows of search symbols.
the present 
3. **Movie Watching**: Participants watched four short movies with different themes, with event markers recording the start and stop times of presentations.




At the ds05505/ level,
each task has the following files:
“task-{Task Name}_eeg.json”
“task-{Task Name}_events.json”

the json’s are schemas (i.e. “column name: description”) for the actual data (recorded in the “sub-” folders)


note that ds05505 marks version 1; version 2 is ds05506 etc
note that version S3 URIs are available (should be able to be accessed via the AWS boto3 library in python); should be able to avoid large download issues locally with partial loading)
release 1 has 136 subjects
release 11 has 430 subjects

per the README, future versions might include: 
* **Future Releases:** We are committed to enhancing this dataset with additional, valuable features in its next stages, including:
  * **Personalized EEG Electrode Locations:** To offer more detailed insights into individual neural activity patterns.
  * **Personalized Lead Field Matrix:** Enabling better understanding and interpretation of EEG data.
  * **Eye-Tracking Data:** Providing a window into the visual attention and processing mechanisms during EEG experiments.

At the ds05505/sub-xxxx level,
note that all sub-xxx folders contain ONLY an eeg folder

At the ds05505/sub-xxxx/eeg level,


4 relevant files:
(example: /ds005505/sub-NDARGJ395FKP/eeg/sub-NDARGJ395FKP_task-seqLearning8target_events.tsv) 
filename
file example
description 
{task}_channels.tsv

(130 rows in this example)
the channels recorded
{task}_eeg.json

details behind the channels recorded 
{task}_eeg.set
*note the .set file is uniquely for recording EEG data, should use MNE python lib

the actual raw EEG data 
{task}_events.tsv

the actual events that occurred during testing (might need to zoom in)
note: I’ve uploaded this sample to this drive folder
each row represents the exact time point the event started
events include:
seqlearning start
learningblock_1
dot_no1_ON
dot_no1_OFF
..
dot_no7_OFF
learningblock_2
…seqlearning_stop
there are 8 dots 
the columns user_answer and correct_answer are only populated for the event dot_no7_OFF; the user guesses the sequence when the last dot is turned off




Using https://mne.tools/stable/auto_tutorials/intro/20_events_from_raw.html 

