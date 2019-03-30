===========================================
Tutorial: How to develop a simple game
===========================================

To help you getting started with creating your own games this section gives step by step instructions for how to implement a so-called Ultimatum Game.

The Ultimatum Game
==================

In an Ultimatum Game the participants play in groups of two. One of them takes the role of the proposer. He gets an initial endowment and decides upon how to divide it between him and the other participant – the responder. The responder then decides whether he accepts the proposal. If he does so, the final payoffs of the participants are according to the proposal. If the responder does not accept the proposal both participants receive nothing as final payoff.

Building the game
==================
To create a new game click on "new game" in the top bar in the overview mode. Type in a game name of your choice and change the availability to "private". Thus other users cannot see "your" Ultimatum Game. Click "save". ClassEx will automatically switch into editing mode and you can start building the game.

Assignment & Matching
~~~~~~~~~~~~~~~~~~~~~~

Go to the tab "assignment & matching". Select "role & group" in the drop-down menu "assignment" and select "2" in the drop-down menu "number of roles". This means the participants in this game are selected into groups of two with every group consisting of one participant of each role. Leaving "partner" as the matching mode means the groups stay together over several rounds of the game.

Stage 1: Proposer’s decision
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go on to the tab "stage 1". In this first stage of the game the instructions for all participants should be on the lecturer’s screen (all participants can see it) and the proposers should decide how much they want to transfer to the responder. The stage should be started by the lecturer pressing a start button. In the first stage we don't have to think about the responder whose decisions will be designed in stage 2. 

First type in a name for the stage, e. g. "UltimatumProposer". "Late arrival" should be "possible". That means, participants can still log in after the stage has been started by the lecturer. 

.. note :: After writing the name of the stage into the empty field and clicking into another field you might have noticed that the page refreshed itself. Doing this it automatically saves every change you make. If you pause designing your game you can just click into another field and make sure everything is saved. Later you can get back to where you left via the overview mode. In the default screen of the overview mode the general folder will be opened. There you find your created game and can open it by clicking on "edit".

The start button is already implemented by default in the first stage in the lecturer field on the right side. To add the instructions click on "add new element" in the lecturer field and select "text box". Click on the little symbol "paste element" on the right side above the start button field to insert the instructions above the start button. 

.. note::  If you want to move an element, you can do this by clicking on the scissors symbol in the element field you want to move. Doing this you cut out the element. You can insert it again in the spot you like by clicking on "paste element".

Change the selection in the dropdown menu in the text box from "display always" to "before start". Now insert the game instructions that should be visible for all participants. An exemple for those instructions could be: "You play with another participant here in the lecture hall. One player in each group gets 10 € at the start of the game. This person is called "the proposer" and decides how to divide those 10 € between you. Then the other person, called "the responder", can decide to accept or reject the offer. If the responder accepts the offer, both will get this payoff. If the responder rejects, both player will get nothing."

.. note :: If you want to have further options for text-editing you can press on the small notepad-icon on the left side of each text field. You can leave again from there by pressing "x" in the top lefthand corner of the box.

Now we start editing the participant’s field on the left side. An input element with one input field and some places to insert text is implemented by default. Change the "Type of input field" to "Numeric input field". Every participant in the role of a proposer will be able to decide upon the amount he wants to keep for himself by entering it into this field. The field "variable names" next to the "Type of input field" defines the variable name. This is the internal name of the variable and will not be visible for the participant. Type in e. g. "keep". Only the proposers should have an input field in this stage while the responder has to wait for the offer. Therefore change the field "for all roles" to "only role 1". In the text field you can insert a description of the input value being visible for the participant. Type in e. g. "For me:". Below the text field you can edit some more settings of the input field. The "Minimum" should be "0" because the responder cannot keep a negative amount. The "Maximum" should be equal to the initial endowment because the proposer cannot keep more than this for himself.

.. Note :: At this point it could be helpful to add fields calculating the amount of money a proposer sends to the responder. These fields could dynamicly display these information to the proposer. When the proposer would enter a "5" in his "send"-field, classEx could display "The amount you send to the responder is '5'". Although this calculation is easy for any participant, it ensures they are always aware of the game mechanism and do not make a calculation mistake. You will learn e.g. how to insert such calculation fields in the chapters on creating own games following this tutorial.

The initial endowment could be a parameter you maybe will want to change in the future. You should only need to change one value to do so. Therefore you should define the initial endowment as a general parameter of the game. To do so you need to add a "program code (subjects)" element (participants field -> add new element -> program code (subjects)). Click on the little paste-symbol above the input field to insert the program field. In the program field you now can define the initial endowment as a variable. Type in "$endow = 10;" for an initial endowment of 10. 

Now you can use this variable to define the upper threshold of the amount the proposer can keep (if you deviate from "10" remember to also adopt your instructions in the lecturer text box). Type "$endow;" in to the "Maximum" field of your Numeric Input Field. Type in "0" into "decimal place" to not allow for decimal numbers and define the "unit" e. g. as "€".

For clarification you should add a more general explanation of the stage for the proposers that is displayed above the input element. Click on "add new element" in the participants field and select "text box". Click on paste between the "program code (subject)" and the input element. Again change the field "for all roles" to "only role 1". Then insert the instructions, e. g. "You decide how to divide $endow; € between you and participant 2. Participant 2 decides, if he accepts or rejects. If he rejects, both of you get nothing. If participant 2 accepts, payoffs will be according to your proposal."

.. Note ::  What have we done by now? 	We are done with assignment & matching and the first stage. So after logging in participants are assigned to groups and roles. The instructions get displayed to both the proposer and the responder. We have a start button and everything prepared for the proposer to participate in the game. In the next two steps we will model the decision of the responder, displaying the results and ending the game.


Stage 2: Responder’s decision
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the second stage the responders are informed about the proposals and they decide whether to accept or to reject.

Also the second stage is already provided by default. Type in a name for stage 2 (e. g. "UltimatumResponder"). "Late arrival" should be "not possible" in this stage, because partners are already matched and newcomers cannot be integrated once the first stage has been played. The first thing we do is to inform the responder about the proposal. To do so you need a "program code (subjects)" field (-> add new element -> program code (subjects)). Change "for all roles" to "only role 2". Type in the following code:

.. code:: php

	$keep = $findVariablePartner("keep",$round);
	$receive=$endow-$keep;

The first line defines a variable "keep" and assigns to it the value of the participant’s matching partner’s "keep"-variable. The second line calculates how much the receiver gets and assigns the value to a variable "receive". Now you can use both new variables to inform the responder about the proposal made to him. Therefore we need to create a new text box in the participants field below the program code field (-> add new element -> text box -> paste element). Change "for all roles" to "only role 2" in the text box and type in the following instructions:

.. code:: html

	Participant 1 has decided to split $endow; as follows: $keep; for participant 1 and $receive; for you. You can accept the proposal or reject it. If you reject it, both get nothing.

Now you need an input element via which the responder can accept or reject the proposal. Insert an input element beneath the text box and insert a "new input field" within the input element. As the responder can only decide between "Accept" and "Reject" we change the type of input field to "Buttons (Single Choice)". Set the variable name to e. g. "accepted" and define the input field as visible for "only role 2". Write a text into the text box that should appear above the "accept" and "reject" button (e. g. "Your decision"). To insert these buttons type "2" into the text field next to "add new possible answer" and click on the little plus left of it. Insert "Accept" and "Reject" into the new text fields. The values assigned to the decision buttons are very important. Choose the value "1" for the accept button and the value "0" for the reject button.

The second stage should start for a responder automatically as soon as "his" proposer has sent a proposal. Therefore delete the "results" field in the lecturer field by clicking on the rubbish bin icon in the top right corner of the field. Then insert an "automatic start" via "add new element". Change the mode to "wait for others". To display how many proposers and responders have already made their decisions on the lecturer’s screen, set the counter to "display" and the count to "by role".

Stage 3: Results
~~~~~~~~~~~~~~~~~

When the responders have accepted or rejected the proposals you can display the results in a third stage. Add a new stage and name it e. g. "Results". "Late arrival" again is "Not possible". The two fields next to the "late arrival" field define how often stages get repeated and where to jump after finishing this stage. Using this you can define the number of rounds you want to play. Choose "back to stage 1" and e. g. "2x" (for repeating the the stages two times).

For both participants the payoff depends on whether the responder accepted the proposal or not. You have to distinguish these two cases. To do so you use two program code (subjects) fields in the participant field. Insert them above the default text box. You need one for "only role 1" and one for "only role 2". The program for role 1 is:

.. code:: php	
	 $accepted=$findVariablePartner("accepted");
	 $payoff=$keep*$accepted;
	 if($accepted==0) {
	 $text="Participant 2 has rejected your proposal.";
	 } else {
	 $text="Participant 2 has accepted your proposal.";
	 }

The program for role 2 is:

.. code:: php

	 $payoff=$receive*$accepted;
	 if($accepted==0) {
	 $text="You have rejected the proposal.";
	 } else {
	 $text="You have accepted the proposal.";
	 }

Afterwards insert two text boxes in the participants field. Again one for role 1 and one for role 2. In these text boxes you inform the participants about their final payoff. For role 1 the text could be:

	You proposed to keep $keep; € from the initial endowment $endow; €. $text; Your payoff is $payoff; €.

For role 2 the text could be:

	Participant 1 has proposed to split $endow; as follows: $keep; € for him and $receive; € for you. $text; Your payoff is $payoff; €.

In the lecturer field you can show the results. Delete the start button that is implemented in a new stage by default. Then add a results matrix element. Change "decision role 1" from "stage 2 # 1" to "stage 1 # 1". Change "count" to "by role" and "display results" to "by round".

Testing the game
=================

Congratulations! You just finished designing your first own game!

To test the game, change into lecture mode. If you already started another game, your self-designed game won't open automatically. In this case you can just "close" the running game by clicking on "select game" in the top bar and picking your "own" game. You can test the game on your own PC without other devices by clicking on "new test participant" in the top bar of the lecture mode. This opens a participant screen in a new tab. You will see the game just as your participants will see it when actually playing the game. You can open as many screens as you want, where each screen represents a participant. After opening enough test participant screens click "Start" in the lecturer screen. Then you can go through the game with all test participants.