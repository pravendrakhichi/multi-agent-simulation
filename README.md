<!-- Copy and paste the converted output. -->

<!-----
NEW: Check the "Suppress top comment" option to remove this info from the output.

Conversion time: 1.561 seconds.


Using this Markdown file:

1. Paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* Docs to Markdown version 1.0β29
* Sat Jul 25 2020 09:47:37 GMT-0700 (PDT)
* Source doc: Project proposal

WARNING:
Inline drawings not supported: look for ">>>>>  gd2md-html alert:  inline drawings..." in output.

* This document has images: check for >>>>>  gd2md-html alert:  inline image link in generated source and store images to your server. NOTE: Images in exported zip file from Google Docs may not appear in  the same order as they do in your doc. Please check the images!


WARNING:
You have 7 H1 headings. You may want to use the "H1 -> H2" option to demote all headings by one level.

----->


<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 2; ALERTS: 5.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>




<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")


**Real-Time Autonomous System**

Pravendra Singh Khichi B16EE026

Zaid Khan B16CS040


# Soccer Multi-Agent Simulation


## **24<sup>th</sup> July 2020**


# OVERVIEW

A soccer game is a specific but very attractive real-time multi-agent environment. In a game, we have two competing teams. Each team has a team-wide common goal, namely to win the game. The goals of the two teams are incompatible. The opponent team can be seen as a dynamic and obstructive environment, which might disturb the achievement of the common team goal. To fulfill the common goal, each team needs to score, which can be seen as a subgoal. To achieve this subgoal, each team member is required to behave quickly, flexibly, and cooperatively; by taking local and global situations into account. The team might have some sorts of global (team-wide) strategies to fulfill the common goal, and both local and global tactics to achieve subgoals.


# GOALS



1. Agent architecture
2. Control collaboration protocol
3. Behaviors of each model
4. Simulation in dynamic action 


# SPECIFICATIONS OF SOCCER GAME

For this project, we will be using the python agent development environment(PADE). It used object-oriented programming concepts with communication through message passing. It also uses a flask to get information about the agents running on the server on port 5000.


# DESIGN

This design is a simple CLI based design where the soccer is simulated with communication between agents through FIPA protocol. We have different agents to deliver different behaviors in the environment. The following are the agents in the environment:



1. Attacker
2. Defender
3. Winger
4. Goalkeeper

All the agents have different behavior which includes passing the ball, attacking the goal post, and defending the goal. For this the agents use different protocols. For example, goalkeeper uses request-response behavior to pass the ball to winger. Then winger uses bidding protocols for passing the ball with possibility that the ball can be intercepted by the defender. If the defender gets the ball then the game will restart. Otherwise, the ball will be passed to attacker. If attacker scores a goal then it notifies every other agent by using the subscribing protocol. If it fails then again the game will start

 

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline drawings not supported directly from Docs. You may want to copy the inline drawing to a standalone drawing and export by reference. See <a href="https://github.com/evbacher/gd2md-html/wiki/Google-Drawings-by-reference">Google Drawings by reference</a> for details. The img URL below is a placeholder. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![drawing](https://docs.google.com/drawings/d/12345/export/png)


# PLANNING SCHEME


## World/Environment

For the simulation purpose, we are using PADE which is a framework for python for development, execution, and management of MAS(multi-agent systems) environments of the distributed computation. It uses the most popular FIPA standard protocols, like ContractNet, Request, and Subscribe.

	The core package consists of basically an agent (has the necessary functionalities for defining an agent and to enable AMS registration, connection verification, and message exchange), an AMS system (for the purpose of communicating), and behavior. 


## Agent Architecture

The Agent Model is composed of a connection mechanism to the platform, a message dispatcher, and a set of different behaviors that the dispatcher gives the messages to. 

Each PADE agent has an internal message dispatcher component. This message dispatcher acts as a mailman: when a message for the agent arrives, it places it in the correct “mailbox” (more about that later); and when the agent needs to send a message, the message dispatcher does the job, putting it in the communication stream. The message dispatching is done automatically by the PADE agent library whenever a new message arrives or is to be sent.

The agent is nothing but a model or actor for our simulation which is responsible for doing the actions in the simulated environment. These are the following agents that we will be having in our design:

GoalKeeper: Its responsibility is to start the soccer game. It passes the ball to one of the team members randomly.

Defender: The task is to take the ball by bidding to the opponents. The bid generated is random. If the bid is enough then it fetches the ball from the opponent and the game starts again.

Winger: The responsibility of winger is to pass the ball to the attacker, where there is a possibility of interception of the ball by an opponent player. So with a probability, it passes the ball to the team.

Attacker: The attacker agent is responsible for attacking with a certain probability. If it scores then everyone will celebrate. And if it fails then the match will start again from the goalkeeper agent.


## Behaviors

An agent can run several behaviors simultaneously. A behavior is a task that an agent can execute using repeating patterns. PADE provides some predefined behavior types: Timed behavior, bidding behavior, publisher-subscriber behavior. Those behavior types help to implement the different tasks that an agent can perform. 

Every agent can have as many behaviors as desired. When a message arrives at the agent, the message dispatcher redirects it to the correct behavior queue. The behavior has a message template attached to it. Therefore, the message dispatcher uses this template to determine which behavior the message is for, by matching it with the correct template. Behavior can thus select what kind of messages it wants to receive by using templates.

The following are the behaviors we are going to use in our design:

Passing behavior: Between members of the same team. It’s just a request-response behavior between the same teams.

Publisher-Subscriber behavior: To notify others that the ball is received, and passed to some other members.

Bidding behavior: To call out for the ball to team members bidding is necessary. Through which defender and attacker will get the ball. 


## Control Collaboration Protocol: FIPA

The FIPA-Request protocol is used when you need to make a request for something to other agents.



<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")


The FIPA-Contract-Net protocol is used for situations where it is necessary to carry out some type of negotiation between agents. In the same way as in the FIPA-Request protocol, in the FIPA-ContractNet protocol, there are two types of agents, an agent that initiates the negotiation, or a beginning agent, making requests for proposals and one or more agents that participate in the negotiation, or participating agents, that respond to the initiating agent's requests for proposals.



<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")


The FIPA-Subscribe protocol implements the behavior of editor-subscriber, which consists of the presence of an editor agent who can accept the association of other interested agents, subscribing agents, in some type of information that this agent has, subscribing to the information and receiving message whenever this information is made available by the publishing agent.



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")



# SIMULATION


# HOW TO RUN THE CODE:

Install the dependencies by pip3 install -r requirements.txt

Then for running the code run: pade start_runtime --port 20000 driver.py
