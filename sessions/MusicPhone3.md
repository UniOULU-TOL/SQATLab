# Instructions
Your home assignment starts Wednesday October 28th, 12:00 EET. The deadline is Wednesday November 5th November, 12:00 EET.

If you are a Microsoft Windows user, please use the Eclipse version available [here](http://j.mp/eclipse4s).

You will also need to use Git in order to get the code base from Github and return it to me. You can download Git from [here](http://git-scm.com/).

Once you have Git installed run the Git client. If you selected the UI version select *Clone existing repository*, and in the first field (*Source*) input https://github.com/<yourusername>/MusicPhone (replace <yourusername> with your Github username).
In the second field (*Destination*) input an empty folder, on your computer, where you would like the project to be copied to.

If you selected the command line version, move to a directory of your choice and input 
*git clone https://github.com/<yourusername>/MusicPhone* (replace <yourusername> with your Github username).  
In both cases you will be prompted to insert your Github username and password.

Git keeps track of the modification you make to the files in the project folder. When you are satisfied with your work you should commit it to your local repository.

To do that, from the GUI version hit *Rescan* (this makes sure that all the modified files will be included in the commit), then *Stage changes*, finally input a commit message in the text area and hit *commit*.  

If you are getting an error message when trying to commit, you probably need to modify your preferences. You can do that from the Edit —> Preferences menu, and set your user and email, finally hit *Save*.  

You should also push (which means send your committed version of the code to the Github online repository), so that I can also see the results of your work. To do that, hit the *Push* button after a commit. You will be prompted for your Github’s username and password.  

The same is accomplished when using the command line by giving the following commands:
*git add <modified files>*, you can use wildcards and input *git add \** as well.  
In order to commit issue the command:
*git commit -m “commit message”*.  
Finally, to push the commits from the command line give  
*git push origin master*.

To make sure that a push succeeded, point your browser to https://github.com/<yourusername>/MusicPhone, you should see your commit message on the page.

More documentation about Git can be found [here](http://git-scm.com/doc).

**For the evaluation: I will take into account the latest commit, before the deadline, visible on your Github repository**. 

For the final home assignment your task is divided into two parts. You need to complete the first part in order to tackle the second one. 
Notice that for the system to properly work, you will need the implementation of the two methods developed in session 6 and 7 in the lab: *computeDistance* and *getRecommendations*.  
You can continue to implement such methods by yourself, following the instructions received during the lab ([here](http://unioulu-tol.github.io/SQATLab/sessions/MusicPhone.html) for computeDistance and [here](http://unioulu-tol.github.io/SQATLab/sessions/MusicPhone2.html) for getRecommendations), or you can copy&paste it from [here](https://gist.github.com/dfucci/406331d6c6bffde6153d) (*computeDistance*) and [here](https://gist.github.com/dfucci/cab3bd45148b7ee87f63) (*getRecommendations*). Be aware, since there are no tests for these methods there could be some bugs.

In case you want to consult the system architecture, please check it [here](http://unioulu-tol.github.io/SQATLab/sessions/MusicPhoneDocs.html)

Please do not touch the UI classes. See Bonus task below.

*If you are using the Eclipse version used during lab, please make sure to start the episodeView plugin everytime you are working on the project. Go to Window —> Show View —> Other and select episodeView in the Other folder on the list. Press the green play button to start the plugin.*

# 1st part - Find concerts for an artists
You will first need to implement the *getDestinationsForArtist* method of the *Recommender* class. 

When the user clicks on an artist’s name in the list of recommended artists, the UI calls the *getDestinationsForArtist* method to obtain a list of *Destination*, where each destination contains the info of an upcoming concert together with the distance to the concert’s location from the user’s current position. 

The user’s current position is provided by the GPS. If the concert's location has an invalid GeoPoint, then the distance should be marked as null. You’ll need to use *IConnector* interface *getConcertForArtist* method, implemented in the *LastFmXmlConnector*, to complete this task. 

# 2nd part - Compute an itinerary for concerts
Implement the *buildItineraryForArtists* method of the *Recommender* class. 

In the UI, the user can click on buttons that will add or remove a selected artist to a list of artists who the user would like to see in concert. Whenever this list is changed, the application recalculates an itinerary of upcoming concerts by calling this method. 

An itinerary is a list of *Destinations*, where each destination contains the concert information and the distance from the previous destination. The first destination’s distance is the distance from the user’s current position. The itinerary must be chronologically ordered according the the start date of the concerts in it. 

Satisfy the following constraints in any order, but tackling them one by one: 
1. The itinerary starts with the concert having the earliest start date for any of the selected artists.
2. An artist has at most one concert in the itinerary (some artists may have no concerts, however).
3. No two concerts in the itinerary may take place on the same day.
4. If multiple artists have concerts on the same day,the itinerary includes only the concert that is closest in distance to the previous destination. 
5. If the same artist has multiple concerts on the same day, the itinerary includes only the concert that is closest in distance to the previous destination. 

# Bonus task
If, and only if, you think you have correctly completed all the tasks in the project you can work on the bonus task.  
For the bonus task you will hook-up the methods you have written so far to the user interface. For example showing the list of artists/destinations in the correct panels, handling the clicks on buttons with the right behaviour, and so on.

