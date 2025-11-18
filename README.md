# Human Experience in Regulated Offices (HERO) study
---
### Objective
The primary goal of this study was to assess how environmental conditions, particularly temperature, impact the perception of comfort and productivity among office workers. The study focused on how personal characteristics affect multi-domain comfort perception by monitoring physiological responses, complemented by survey-based validation.


### Method
A total of 24 participants were involved in the experiment study. Each participant was required to perform a series of four activities in sequence reading, writing, discussion, call in an office setting, with two participants present at a time in the office room. The experiment was conducted in two seperate sessions under different temperature conditions: low (22°C) and high (30°C). The temperature was the only environmental variable altered between two sessions while the activities sequence remained similar. Each session was paired with a different reading content to ensure variation in the cognitive tasks while maintaining the activity occurance.


**Activities:** Participants were asked to perform the following four tasks in both the low and high temp conditions:
1. **Reading**: Reading an article on a specific topic.
2. **Writing**: Writing a summary based on the article they had just read.
3. **Discussion**: Engaging in a discussion with a colleague about the same topic.
4. **Conference Call**: Participating in a conference call to further discuss the topic.

![Study overview](https://github.com/tomarp/HERO/blob/main/metadata/HERO_Overview.png)


### Design

The sequence of events occurance during each session was as follows:

1. **Perception Survey (Initial)**: Participants first completed a perception survey, which assessed their comfort levels across multiple domains, including:
   - Productivity
   - Thermal comfort
   - Air quality perception
   - Acoustic comfort
   - Visual comfort

2. **Activity 1 (Reading)**: Participants then began the first activity, reading an article.
   
3. **Perception Survey (Post-Reading)**: After reading, they completed the same perception survey to gauge how their comfort perception might have changed.

4. **Activity 2 (Writing Summary)**: Participants proceeded to write a summary of the article they had just read.

5. **Perception Survey (Post-Writing)**: Once again, a perception survey was administered to capture their comfort levels.

6. **Activity 3 (Discussion)**: Participants discussed the article with a colleague.

7. **Perception Survey (Post-Discussion)**: They filled out the perception survey for the third time after the discussion.

8. **Activity 4 (Conference Call)**: Finally, participants engaged in a conference call to discuss the topic further.

9. **Perception Survey (Post-Conference Call)**: After the conference call, the final perception survey was completed.


### Device


**EmotiBit:** is a wearable sensor platform designed for real-time physiological data collection. It typically attaches to the back of an existing wearable device, such as a smartwatch, and measures a range of biometric signals including:

    - Electrodermal Activity (EDA): Measures skin conductance, which is associated with sweat gland activity and can indicate psychological or physiological arousal.
    - Electrocardiogram (ECG): Measures electrical activity of the heart.
    - Photoplethysmography (PPG): Measures blood volume changes, commonly used for heart rate monitoring.
    - Temperature: Measures skin temperature.
    - Accelerometer and Gyroscope: Measures motion and orientation.
    - Inertial Measurement Unit (IMU): Combines accelerometer and gyroscope data to capture movement in 3D space.

**Muse:** The EEG data files for participants in cold (trial A) and hot (trial B) conditions. Each dataset contains the following columns:

    DateTime: The timestamp for each EEG reading.
    tp9, af7, af8, tp10: EEG channels with recorded signal values.
    Activity: The activity performed during the recording, which could provide context for event-related changes.

    tp9 and tp10:
    Located near the temporal lobes.
    Important for analyzing brain activity related to auditory processing, memory, and emotional responses.
    
    af7 and af8:
    Located near the frontal lobe.
    Crucial for studying cognitive processes like attention, problem-solving, and emotional regulation.

EEG frequencies above 50 Hz are typically less useful for analysis as they often consist of noise or muscle artifacts.

## Dataset 
Link to the dataset: [Zenodo](https://zenodo.org/records/17597414)

Throughout the experiment, a comprehensive set of data was collected across multiple channels:


**Physiological Data** The data column contains the following physiological and device signals:

    acx, acy, acz: Accelerometer data along x, y, and z axes.
    bat: Battery level of the device.
    eda: Electrodermal Activity data.
    edl: Probably Electrodermal Level or some related measure.
    gyx, gyy, gyz: Gyroscope data along x, y, and z axes.
    mgx, mgy, mgz: Magnetometer data along x, y, and z axes.
    pgg, pgi, pgr: Possibly related to photoplethysmography (PPG) or other physiological signals.
    thr: Could be related to a threshold or temperature measurement.
    device_address and user_id: Metadata related to the device and user.


**EEG:** Collected EEG (electroencephalogram) data to monitor brain activity during the tasks.
Columns in the Dataset:
        user: Identifier for the user, in this case, it's always 'S01A'.
        tp9: EEG channel data from the TP9 electrode.
        af7: EEG channel data from the AF7 electrode.
        af8: EEG channel data from the AF8 electrode.
        tp10: EEG channel data from the TP10 electrode.
        ts: Timestamp associated with the EEG recording, represented as a floating-point number.

    Data Types:
        All EEG channel data (tp9, af7, af8, tp10) are of type float64.
        The ts (timestamp) column is also of type float64.
        The user column is of type object.

Initial Observations:

    The EEG data has a high sampling rate given the large number of entries.
    The dataset includes four main EEG channels (TP9, AF7, AF8, TP10) with corresponding timestamp data.

**Survey Data**: Responses from the perception surveys completed before and after each activity.

**Environmental Data**: Sensors recorded real-time data on temperature, humidity, and other environmental parameters in the room.

**Video Data**: Webcam recordings of the participants' activities and their conference calls.
