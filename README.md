# freelancer_job1
repository for freelancer work

#Task - Scope
- Update CamionComponent.vue to show 5 tanks (current file has 3 tanks), leveraging the Vue/Vuetify Grid System
- Make the view responsive, adjusting to size changes (specially the  tank images in background) 
- fix a couple of formatting bugs

#Description / Explanation
- this component is used by a larger Vue application to monitor a beer installation
- Screenshot picture of the 3-tank-component added for reference: only top section of CamionComponent (the image with the tanks) is of interest here. Other Subcomponents used further down the page are not included here.
- subcomponents that are in fact being used and elements (like images) requiered to paint the view, are added to the repository. 
- variable values are read from a firebase database (code not addded to the repository) and added to CamionDatos: >> same datastructure and access to the variable values would be availabe for the 5 tank configuration, so methodology can be replicated for 5 tanks, chaning the index.

#Other itmes & Bugs to be fixed:
* Line 31: i have not been able to force fonts size or color for text or icon:  please try to do so (color white, fontsize 8px, when alarms)
* in the tank component rendering, the tank imagen is split (top, middle, bottom), and it does not properly match the 3 subpictures (top middle, center, bottom) for (see sample screenshot in Issues)... please fix so that diagram is ok.
* 

#Final requests / recommendations
- update the code to enable a cleaner, more manageable code: currrntly it has a rather frankenstein type of code, with plenty of commennts, being used for debugging
- streamline the styling with classes
