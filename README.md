We have an application that we want to improve by providing the users with a way to create
events. Users should be able to create an event, invite people, and receive an RSVP.
Provide an ERD showing the new database tables/fields necessary to implement this
feature. Then, briefly describe how your model handles recurring events including the
positives and negatives of your approach.

#Assumptions

 - No code.
 - Basic recurring intervals vs special cases ex. "last Thursday of every other month."
 - Basic tables to prove concept vs entire application ex. message handling and notifications.

#How it works

- When a user creates an event the event data gets saved to the Events table. I left it as a not user is tied to an event directly in the Events tables but instead an EventRSVP is created for the user that created the event with the role of "Host" and RSVPType of "Going." The fields for the role and RSVPType is an Id that has been normalized to it's own EventRoles/EventRSVPTypes tables for less redundancy. (not completely necessary)
- Recurring is implemented here as a way to add multiple recurring times per an event. When an event ends the EventIntervals table will be parsed for the current ending event Id and gather all intervals available. 
- Formula (in word explanation, why not equations?): The end-time substracted by the date-created and coverted to minutes will give the highest amount of minutes to current date. Using the modulus operation you can take the highest amount of minutes and "mod" by the highest interval to get the latest intervals rotation. Then loop through available intervals for the lowest value interval that is greater than the current leftover minutes. 
- Update the event start and end time according with the new date based on the next interval.
- If you would want to keep records of everyone that went to each recurring event forever there would need to be some changes like creating a past events table or something of the sort to link RSVPs to. 
- Everything is always up for some good discussion and brain expansion since this was done quite quickly.

#Installation

- git clone https://github.com/JohnPittman/orgsync-interview-test-erd.git

#Contents

- events-erd.png: exported image of the ERD from MySQL Workbench.
- orgsync-events.mwb: MySQL Workbench original file.