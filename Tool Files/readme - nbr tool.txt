This doc is a bit old, needs to be updated..........   Jul2013

NOTE: to show thermatic grids for KPIs and traffic, you just add those kpis to your import file and use the IDW interpolator, use an exponent of 7-10 and make the cells large relative to the intersite distance, like 30-50% of it.  Then you get better results.  It really depends on what you are mapping
---------------------------------------------------------------------------
---------------------------------------------------------------------------

This is an RF planning/deployment/optimisation tool for mapinfo, it can take up to 5 separate systems.  
It works fine with up ~ 10,000 sectors.  Beyond that it starts to slow down.  It has been used with up to 50,000 sectors, but doing nbr editing gets quite slow in that case.  Recommend keeping cells below 10,000, it is very fast if the cell count is below 3,000

=> Nbr intra/inter System Visualisation and Editing with the mouse.  Changes are written to the CR file.

=> Comprehensive cell parameter editing (site name, site id, cell id, sc, azimuth, ht, edt, mdt, status, lat/lon).  These changes will be updated in your databse as well as written to a CR file to highlight changes made that session.

=> Perform various cell editing functions with the mouse, such as change azimuth, move cell/site, move can be whole site move to final location (shift - one cell) (ctrl - whole site shift by dragged amount), delete (shift is cell, o/w whole site), add sites

=> Analyse pn/sc/freq.plans visually/manually or automatically, find co/ajd cells and find cells by cell_id, name, sc, bcch etc., can also copy paste host:nbr:nbr... and view directly on the map

=> Nbr Pair Visual Review feature... Tool imports a list of nbr pairs to analyse and allows the user to simply step through the list while tool zoom and highlights each pair in question, makes review of grey area pairs quick

=> Define the different status values assigned to cells/sites and can save these along with the display settings in a project file that can be loaded/saved at anytime.

=> Nbr Statistics Visual Review, Tool can import and process nbr2nbr stats intra/inter system and display them graphically, also allows the user to view individual pair stats and edit the desired nbr edit action

=> Drive Data Visual Analysis Feature, Tool imports RF top N drive data from scanner/phone (lat/lon/bcch-bsic-rxlev/sc-ecio-rscp), auto creates best server (bcch-bsci, sc, rxlev, ecio, rscp) and also creates individual cell rxlev/ecio/rscp as the user clicks on a cell

=> Nominal RF Quick Design Feature using the hexagon feature, draws the cells as hexagons and will place them freely or snapped to grid.  

Note on the snap2grid feature
When placing or moving cells, if the snap to grid feature is on, the site will auto-snap to other sites with exactly the same 
cell-size and az parameters if the new site/moved site is put close to these sites.  The snap2grid feature will NOT snap to other 
sites if they have different azimuths or sizes

Note on cell sizes
In Hexagon mode, the obj_size column is used for:
		1) 	the hexagon diameter for normal cells
			#in a normal sectorised hex array => the hex diameter = Intersite Distance x 2/3 (ISD x 0.6667)
		2) 	the hexagon diameter for omni cells
			#in a normal omni hex array => the hex diameter = Intersite Distance x 2/sqrt(3) (ISD x 1.1547)
		Thus when drawing in Hex mode, the ISD (intersite distance) = Obj_Size x 2, thus Hex diameter = Obj_Size x 4/3 for sectors and Obj_Size x 4/sqrt(3) for omnis

In Cell Pies Mode, the obj_size col is used for just representing the cells as opposed to an geometric design feature:
	1) the pie radius for normal cells
	2) the circle radius for omni cells (reduced by the omni reduction factor)


=> Draws the cells for you from the input file and you can resize and recolour the cells on the fly, without having to re-import them to the tool.

=> Both the CR form and the current cell database can be exported (ready for re-importing) after modification.  

=> The standard input is a tab delimited .csv file with the following column headings(columns can be in any order):

----------------------------------------------------------------------------------------------
Site	Sitename	Cell	System_Index	System	Status   PCI_SC_Bcch_PN	ZCRS_BSIC	ZCRS_Cnt	Lon	Lat	Az	Ant_HBW	Ant_type	MDT	EDT	Ht	Obj_Size	Comment	N1	N2	N3	N4	N5	N6	N7	N8	N9	N10	N11	N12	N13	N14	N15	N16	N17	N18	N19	N20	N21	N22	N23	N24	N25	N26	N27	N28	N29	N30	N31	N32	GSM_N1	GSM_N2	GSM_N3	GSM_N4	GSM_N5	GSM_N6	GSM_N7	GSM_N8	GSM_N9	GSM_N10	GSM_N11	GSM_N12	GSM_N13	GSM_N14	GSM_N15	GSM_N16	GSM_N17	GSM_N18	GSM_N19	GSM_N20	GSM_N21	GSM_N22	GSM_N23	GSM_N24	GSM_N25	GSM_N26	GSM_N27	GSM_N28	GSM_N29	GSM_N30	GSM_N31	GSM_N32
----------------------------------------------------------------------------------------------

NOTE1: 	Site 		is a site id (alpha-numeric) - max of 100 chars
	Cell 		is for the cell_id (alpha-numeric) - max of 30 chars
	System 		= whatever you want(except no ./":()* etc characters), if a system is GSM, make the system type GSM so you can do bsic-bcch analysis, can be up to 10 different systems
	Status 		= Can be anything, the default values are: On-Air, Fault, Integrated, SITAC OK, Waiting SITAC, Need Rehunt, Planned or Other, but you can import anything, you will have to define these status values in the tool though, they will not be automatically created.
	PCI_SC_BCCH_PN	= the pn offset, the sc or the arfcn of the bcch, must be a number
	ZCRS_BSIC	= ZC logical Root Seq index (0 to 838) or BSIC (is in octal => 2 digits 1st from 0-7 and the 2nd from 0-7), must be a number
	ZCRS_Cnt	= how many ZC root seq are needed for this cell, must be a number (0 to 838)
	Lat and Lon 	are in decimal (any projection), must be a number (for lat lon, it doesn't support always +ve numbers => 1.43N and 1.22S, it should bce  1.43 and -1.22) 
	Az 		is azimuth in degrees, must be a number
	Ant_HBW 	is the horizontal BW of the antenna pattern => affects the pie width when drawn, must be a number
	MDT and EDT 	are downtilts in degrees (doesn't affect anything), must be a number
	Ht 		is ant. height in m, must be a number
	Obj_Size 	is the pie radius in m, must be a number
	Comment 	is for arbitrary comments, max of 300 chars

-------------------------------------------------------------------------------------------------
The nbrs are stored in a column based DB, can be up to 10 different systems
-------------------------------------------------------------------------------------------------
	Host_Cell, Host_Sys, Nbr_Cell, Nbr_Sys



Functionality
-----------------------

Buttons
----------
The tool has a button pad with 12 buttons, each has a self explanitory help message, here is a summary:

Button 1: 	import => lets you import your database .csv file, mapinfo sites and cells are created for your database enabling you to visualise your network quickly.  If you have entered site status information,the sites and cells which are on-air will have a different colour to those that are not.
Button 2: 	export => lets you export you latest databse to .csv (which can be re-imported again), it also lets you export the change_request table to .csv which has a summary of all the nbr additions/deletions made during this session.  It also has a summary of any other cell parameter changes made such as azimuth, ht, edt or mdt.
Button 3: 	neighbor edit allows you to visualise the current 3G:3G and 3G:2G and 2G:2G nbr lists and it lets you add and delete nbrs quickly.
Button 4: 	cell edit enables you to click on a cell and bring up it's important details and it allows you to change any and immediatly update the map (azimuth, pie radius, HBW, status, comments, mdt, edt, sc), shift and click brings up info on all the cells in the site and lets you edit them.  Press SHIFT and clicking on a cell will bring up the details of all sectors on the site and allow you to change anything.
Button 5: 	find co/adj pns/scs/bcchs => this tool allows you to click on a cell and immediately see the other co-pns/sc/bcchs or adj-pns/scs/bcchs (to change between co and adj mode use button 10.
Button 6: 	Area redraw allows you to click and drag a rectangle to select several cells at once.  You then can choose how to adjust the display of these cells => like pie radius change or HBW change.  This saves you having to change it globally (good for resizing drawn cells in city centers and rural areas).
Button 7: 	Connector lines => allows you to turn connector line drawing on or off => connector lines can be useful when viewing nbrs or co/adj scs.
Button 8:	Global redraw => the same as the area redraw except it applies you cell size chages to the whole system.
Button 9:	Mutual toggle => turns mutual nbr analysis on/off.  When on, reciprocal nbrs are added for you as well as to the change request table.
Button 10:	Co/Adj toggle => toggle between co pn/sc/bcch search mode and adj sc/pn/bcch search mode
Button 11:	Change Drawing Style => this enables you to modify most of the cell, site, label, neighbor and connetor line drawing styles so that you can customise the tool to your liking.  You can save your preferences to a .prf file of your choice for reloading later and you can reload the default settings fromo the default.prf file that come with the tool.  
Button 12:	2G toggle => this turns the 2G system on/off => if off the 2G system is not visible and no nbrs are shown

Button 13:	Import 2G scan data => this will import a .csv file containing 2G scan data.  The file must contain lat and lon(remember TEMS doesn't export lat/lon correctly when you export to .tab, you need to export to mapinfo and then update column from the objects it creates)  comlumns and it must contain 3 columns for each measurement (BCCH_x, BSIC_x, Rxlev_x) starting with BCCH_1 etc.  The tool will accept up to as many measurements as you wish.  The initial import processing is involved and takes a while so be patient, when it is done, creating specific BCCH_BSIC plots will be very fast.
Button 14:	Show specific BCCH_BSIC plot by clicking on that particular 2G sector.  Obviously this only works if you have the correct frequency plan in the tool.  The output is a thermatic map of the Rxlev of that particular BCCH_BSIC.

Button 15:	Import 3G scan data => this will import a .csv file containing 3G scan data.  The file must contain lat and lon (remember TEMS doesn't export lat/lon correctly when you export to .tab, you need to export to mapinfo and then update column from the objects it creates) comlumns and it must contain 3 columns for each measurement (SC_x, RSCP_x, EcIo_x) starting with SC_1 etc.  The tool will accept up to as many measurements as you wish.  The initial import processing is involved and takes a while so be patient, when it is done, creating specific SC plots will be very fast.
Button 16:	Show specific SC plot by clicking on that particular 3G sector.  Obviously this only works if you have the correct SC plan in the tool.  The output is a thermatic map of the RSCP or Ec/Io of that particular SC.

Button 17: This allows you to move the entire site, or just 1 cell (if the shift button is pressed), NOTE: pressing the ctrl button will make the move based on the vector dragged, not pressing the ctrl button will move the site center to the point dragged to, you only need to click on part of the cell to move the site/cell, not the site symbol

Button 18: This allows you to undo the last cell/site move

Button xx: This allows you to delete a whole site (click on a sector with the shift button pressed) or just one sector (just click on a sector).


Right-Click Functions
-------------------------
search for cell/pn/sc/bcch:  if you right click on the map and choose this function, you can choose what 3G and what 2G parameter to search for (site_id, sitename, cell_id, pn/sc or bcch+bsic)  You can also copy 3 cells from excel (SC, bcch, bsic the ouput of the 2g3g scanner-nbr list creator tool) and paste them into this form to find the different matches.  If you search for site name, you can just put part of the name and it will search for all sites with possible matches.

nbr edit tools - These are available when you have the nbr edit button active:
choose new host:	when you click on a cell, this cells nbr list is shown
add nbr:		when you have an active host, if you click on a cell not in the nbr list, it is added (1 way or mutual depending on your current settings) and put in the change request table
del nbr:		when you have an active host, if you click on a nbr, it is deleted (1 way or mutual depending on your current settings) and put in the change request table

This tool works if you want to analyse 3G only or 3G:2G together.
