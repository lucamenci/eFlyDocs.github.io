<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>


<img src="/img/6dof.jpg" width="400" />


Golf putting is, from a physical point of view, a rather complex phenomenon. 
To reach a reasonable understanding it is necessary to divide it into simpler parts and then reassemble them according to the principle of superimposition of effects. 
Even before that, however, we get rid of some physical aspects which, although present, can be defined as of secondary importance with respect to the heart of the matter.
The putt in golf, even if apparently simple, is, from a physical and mechanical point of view, a rather complex phenomenon. To understand its essence, we must first introduce what we want to measure and how.
The geometric and physical quantities that Capto measures need a reference system to which they can be referred.
This step is more delicate than you think.
In the world of golf, many technologies are in use for measuring the movement of the club or ball. 
Deepening the reflection for a moment, we can see how all technologies of a certain accuracy are characterized by the presence of a fixed measurement station on the ground. 
We define these as Anchored Base measurement Systems (ABS).


## Coordinate System


### ABS - Anchored Base Systems

The anchored base systems use a reference system fixed to the ground which is integral with the base itself. The station is placed on the ground, it is calibrated and then the object to be measured is calibrated with respect to the base itself. 
Ball tracking radars, club tracking optical systems, ultrasonic putt systems and so on are all such systems. 
This approach is extremely advantageous from an instrumental point of view. 
The fixity of the system is not subject to any perturbation and the origin and orientation of the reference system are guaranteed if the two fundamental conditions of not moving the base and not moving the position of the ball are met.
In our laboratories we use ABS systems for Capto control and testing. 
For example, we have built a system for the accurate measurement of Path and Arc, using a high frequency LIDAR chamber placed on a robotic arm that frames the space where the shot takes place. The marker is tracked with millimeter accuracy and precision. The measurements obtained are certain and not subject to perturbations of any kind and for this reason the trajectories measured in 3D can be taken as a certain reference for the same ones calculated by Capto. 
So, since measuring in ABS systems is very simple, why doesn't Capto use the same method?

### Capto System

Capto was born as a real technological challenge. In fact, it aims to overcome the limitations of ABS systems by means of a total paradigm shift.
The first step was to transfer all the sensors necessary for the measurement on board the object to be measured. 
The electronic board itself has been reduced to a weight of five grams. 
The rest of the fifty grams of Capto are due to the box and mainly to the battery.
Moving the sensors on board required a great technological effort of miniaturization which, however, is only the beginning of the work. 
The second step is in fact to transfer the data acquired on board into a reference system virtually integral with the ground. 
The term "virtually" is decisive. This allows us to be able to transfer it all at once, brilliantly exceeding the limit of the fixed station.

There is a certainty in the game of golf: the player will never find himself playing twice from the same point at the same distance. 
In truth this can happen on the pitch following a penalty, but I would say it will never happen on the green. 
This consideration immediately prompted the search for the possibility of continuously varying the playing position, leading to a considerable computation complication on our side as designers 
but which proves to be extremely potential for the user who intends to investigate his golfing technique carefully.

### How  Capto virtual Coordinate System (CCS) is generated

<img src="/img/wcs.jpg" width="400" />

#### Origin of CCS Capto Virtual Coordinate System

We now define the origin of the Capto reference system. Let's imagine a vertical plane passing from the center of the ball and from the target. 
This plane cuts meets the equator of the ball at two points. The furthest point from the target is the origin of the reference system.
At this moment the first big problem arises but which is also a great opportunity compared to ABS systems. For these, in fact, the position of the ball is in effect irrelevant for data acquisition. 
Even for many of them it is possible to acquire the shot even without the ball being present. But we know that positioning the ball correctly with respect to the stance is a fundamental step for the good execution of the putt. 
Basically, the player who trains on an ABS station always addresses the same position and has no way of analyzing this aspect of his technique. 
In Capto this aspect is completely different. The origin is on the point of impact and the displacement of the ball thus becomes important for the estimation of angles and trajectories.
But how can Capto precisely define the point and instant of impact? We must imagine that having no fixed reference station, the sensor has no reference to know where it is and what it is doing. 
The internal software therefore remains constantly listening to the accelerometric and gyroscopic values ​​collected by the sensors. 
It maintains a five-second history of all sensory data in place. 
This is because we do not yet know if we are in the process of making a putt or if the player is simply moving the putter.

The continuous flow at 600 Hz of the inertial values ​​is analyzed by the internal "Impact Detection" module. 
This software segment is based on a proprietary [machine learning](https://en.wikipedia.org/wiki/Machine_learning) algorithm that is able to distinguish random movements or accidental bumps from real putts.
Capto users have noticed how effective this system is. Of course, it is also necessary to understand the criterion with which it works to avoid making evaluation errors. Let's go back to the ABS systems for a moment. 
For these the reference system is fixed and they have no need to interpret anything. So the measurement takes place directly without any prior analysis. 
In the case of Capto, the measurement is carried out only downstream of the interpretation of the data as a shot. For this to happen it is necessary to train * machine learning * with a laborious and complex process of [training](https://en.wikipedia.org/wiki/Training,_validation,_and_test_sets)
We basically have to teach Capto what a put is and what it isn't.

This teaching work began with early versions of Capto and will likely continue until Capto is developed.
It happened, even recently for example, that certain particularly sharp shots were not recognized.
It also happened that a user reported that he was unable to acquire the shots performed with one hand. Obviously, not knowing the mechanism of machine learning, he could not guess why as we designers could imagine this need could exist.
 After an integration into the training process, they too have been successfully acquired. But why is the system so demanding? 
 The answer is reliability. In fact, if we restrict the field of existence of real shots, we avoid acquiring false shots that can make the user nervous. 
 Not surprisingly, in order to acquire shots with great yips, a specific setting is provided that broadens the tolerance range of the sensors.
 The moment the _Impact Detection_ module recognizes the impact, the previous history is analyzed using the _Takeway Detection_ module.
This also works in Machine Learning. It is expected that before the start of the putt there will be a short stop period. This too must obviously be understood by the user. 
Finally also the finish using the _Finish Detection_ must be correctly interpreted and this as well as Impact and Takeaway is continuously improved by further training.
From what has been said it is understood that Capto foresees a certain _syntax_ in the execution of the shot but also that this syntax is the one commonly used by players.


#### Axes of CCS Capto Virtual Coordinate System

We define the main direction which is the one that is taken as the target direction. The other two are a consequence of the first. In fact, the first axis is oriented towards the target, the second is horizontal and perpendicular to the first, oriented to exit away from the player. 
The third is vertical upwards.
So let's start by defining the direction of the first axis, the one that determines the zero for the angles and directions.
This is certainly the most delicate point to explain. The reasoning is quite complex and requires some attention.
Let's proceed step by step.
The Capto module has its own internal reference system. The axes of this system are approximately aligned with the box. Any misalignment is corrected by the factory calibration. 
Recalibration requires special support which can be requested from [Captogolf](https://captogolf.com/capto-contact-information) 
but is generally not recommended unless the module has suffered a really large shock or a actual need.

The sensor module is free to rotate on the shaft and the user must be able to align the box to be congruent with the direction of the putter face. 

<img src="/img/CaptoAlignment.png" width="300" />

It is advisable to have the "Calibration Tool" to perform this operation.

<img src="/img/calibration_install.png" width="500" />

Once the alignment we proceed with the definition of the alignment with respect to the target if necessary.
The opportunity to change the frame of reference from putt to putt can be seized if the direction of reference is also taken as a dynamic. 
The player, at the time of the address, assumes as correct the direction of aim towards which he intends to play. 
If we take the direction as correct we can consider the direction of the face at the takeaway as a reference for the calculation and subsequent graphing of the game parameters. 
Let's explore this topic for a moment. 
The player intends to play in the direction he takes at the address and therefore it is correct to express the numerical values ​​with respect to that direction. 
There are many possibilities that the direction taken is not the same as the target. This circumstance occurs whenever the aiming direction is non-zero. 
But aiming is not a property of the swing technique, but rather a visual one. 
The aiming correction procedure therefore cannot take place in the same session as the correction of the technical parameters of the swing. 
Borrowing from what happens in ballistics, first we fine-tune the mechanical correctness of the weapon which must not have intrinsic manufacturing defects, 
after which we deal with aiming, wind effect, height differences and so on. Therefore, in the aiming correction phase, the player will rotate as much as possible in a monobloc 
by modifying only the position of the feet while maintaining his own playing technique unchanged.
Keeping the technique separate from aiming is central to the error minimization principle. Separate component analysis leads to immediate identification of the defect with subsequent correction. The aim is in fact subject to transitive phenomena of which the brightness and the reading of the slopes are the most important.
Keeping the technique constant allows you to overcome these difficulties while preserving the fundamentals for subsequent situations.
In summary, we can identify the following two points as basic for identifying the direction of the correct reference system.

At Sensor Setup| Putt by Putt
-------------|------------
Sensor to Face Alignment|Take care of face position at Takeaway

What does a possible misalignment entail? We distinguish the two cases. 
The first occurs when the sensor is not properly aligned with the face.
If the sensor is misaligned with respect to the face all shots will be subject to a constant deviation of the Path due to this cause. 
Particularly for a right-handed player, a clockwise rotation of the sensor by two degrees generates counterclockwise rotation of the path by the same amount. 
The veceversa is also valid.
So the assembly error generates a systematic error independent of the shot or the player and the error essentially affects (we can say almost exclusively to less than second order decimals) on the Path.
The second occurs when the player does not take note of the fact that the direction of reference is that taken at the takeaway. 
This means that if the player does not refer visually and mentally to the position of the face at the address, he cannot correctly interpret the numerical values ​​proposed by Capto. 
In fact, Capto cannot take into account the _real_ direction to the target as (unless the "Aim" option is used) as it does not know it. 
Capto knows the direction at the takeaway, takes that as the target direction and presents the game values ​​with respect to it. The step is very simple but sometimes deceives non-regular Capto users. 
Let's take the example of the player who plays at a specific hole, without aim and with a position at the address not aligned with the target. 
Let's suppose that the putts are all in the hole (impact face objectively directed towards the hole) but that, obviously, the face and path values ​​are clearly off target. 
This, which is apparently an inconsistency, hides a great opportunity for game improvement. The hole actually becomes part of the measuring instrument and we explain how. 
The fact that the ball goes into the hole is an objective fact that the face on impact is correctly oriented but the face values ​​of Capto tell us that the position at the address is not correct. 
The method therefore foresees that the position at the address of the face is progressively modified until the Capto values ​​are brought to zero, constantly keeping the ball in the hole.
Summarizing we can exemplify as follows:

Affect|Sensor to Face alignment Error | Takeaway Face to Target alignment Error
------|------|
Face|No Effect|Same Value, Opposite Sign
Path|Same Value, Opposite Sign|Same Value, Opposite Sign

A question that is spontaneous to ask is related to the influence that a possible error in the estimation of the path can have on the final outcome of the stroke. 
To answer this we can rely on what emerges from the experimental analyzes regarding the influence that path and face have in the composition of the launch direction. 
It should be noted that if the path has some influence on the direction of throwing, this depends only on the friction between the face and the ball. If there was no friction, the ball would start in the direction defined by the face. 
By decreasing the friction, the influence of the path decreases, which however averages around seven percent without ever going beyond ten or below five.


.|Face Direction|Path Direction
--|----|---
Weight On Launch Direction|93%|7%


For simplicity we neglect the secondary influences such as that of the lie composed with the loft and that of the deflection following the impact: we can thus attribute 93% to the face and 7% to the path. 
Let's assume a putt with zero degrees of open face and 2 degrees of closed path estimation error. 
The launch angle will be 0.14 degrees which is unable to get the ball out of the hole to ten meters. 
The technical components have the weight they deserve based on their real influence on result.



#### Aim Module

The aim module allows you to orient the main axis towards the physical target. 
The line that defines this axis connects the center of the ball with the physical target of reference. The face and path values ​​refer to this axis and no longer to the direction at the time of takeaway. However, change values ​​are available. Using the aim function complicates the technical analysis and operation of Capto. 
In fact, one cannot ignore setting one or more targets and the position of the ball.

#### A reference for Loft and Lie

Loft and Lie are two angles that express the inclination of the putter out of the plane in the frontal and lateral directions.
As we all know, loft is the orientation of the face in the vertical direction. 
Putters usually have a loft angle just such that, by arranging the shaft vertically with respect to the frontal direction, the putter face appears on the ball more or less inclined upwards. 
By convention we mean the angle that the shaft assumes with respect to the vertical as loft and the same angle to which the angle of the putter is added as dynamic loft. To avoid misunderstandings we prefer to call this shaft angle simply _shaft_. As for the other angle with respect to the ground, that is the lie, the difference with respect to the physical inclination of the putter shaft is assumed to be zero, which usually is around 70 degrees. 
As can be clearly understood in these conventions there is a lot of confusion.

To slightly complicate the understanding of these angles, there is the tendency for some players to assume particular postures that determine the inclination of the shaft axis to values ​​other than conventional ones. 
In particular as regards the loft there is a tendency to incline the shaft in order to advance the grip towards the target. 
This technique, which takes the name of deloft, decreases the effective loft of the face so that the loft of the putter is modified, increasing it, to obtain an adequate dynamic loft on impact. 
Same thing for the lie which sometimes has to be modified from the standard 70 degrees to adapt it to the player's upright or flat trend. Analyzing the issue from a technical point of view, what appears evident is the tendency, or rather, the will, of the player to go back to where he started. 
For this reason we have introduced in Capto the possibility to calibrate the zero on the natural playing position. By this we intend to make the player and / or his coach assume the structure personally considered correct, register that position and assume it as zero. 
In fact, it involves tilting the axis in order to simulate the use of a putter fitted to the player. 
The fitting values ​​are highlighted and the numerical values ​​and graphs are presented relative to the virtual putter thus generated. 
The advantage is considerable as the player has the possibility to work on his own technique with graphs around zero, even using a putter not yet fitted for him. 
This system favors the adaptation of the putter to the player avoiding the bad tendency of adapting the player to the putter he is using.
















