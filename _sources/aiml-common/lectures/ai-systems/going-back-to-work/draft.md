# Back2classroom problem statement. 

To describe the problem more formally, we will use the following terms and notations

### Terminology and Notation

| Term   | Definition  |
| --- | --- |
| Host (ID) | A host can be an enterprise, building owner, space owner, school etc. A host is the account owner of the SaaS app  and via access rights she can adjust the total available capacity and other parameters that affect the policy. |
| Site (ID) | A host is responsible for the management of multiple sites. A site can be a building. |
| Resource (ID) | A site has multiple resources that are managed by the application. A resource can be a floor or a room where multiple actors need to use at the same time.  |
| Resource Type | A resource is associated with a resource type based on a set of attributes. For example, a resource can be of type 'classroom' or 'open floor plan'. | 
| Actor (ID) | An actor is a person that requests admission in the physical space managed by the host. Each host is assumed that is associated with an identity management system that uniquely identifies all actors (e.g. students) or can assign temporary actor identities to ephemeral actors (e.g. customers). |
| Actor Type | An actor has an associated type that is an attribute that can qualify differentiating treatment by the system. |
| Agent | The agent is the AI system that makes the admission decision |  
| Group | A list of actors that request joint admission. | 
|  $C_r$   |  Maximum available capacity / occupancy per site per resource.  $C_r$ is determined by the host based on square footage of the resource and the social distancing guidelines the federal / local governments impose. As the guidelines are time varying, $C_r$ is also time varying and this further qualifies the problem as sequential. $C_r$ is effectively dependent on a fictitious single knob that results into a distinct $C_r$ for each resource. |


### Problem Assumptions

To simplify the problem,

1. The departure times cannot change dynamically. This means that if the actual demand is lower than the predicted demand when the scheduling decision took place, the departure time stays fixed. Employees / customers can extend their departure by sending another request via the messaging app but this is an independent reservation and is not unaccounted for the decision policy. 
   
2. Although this can be very useful for stores and co-working spaces, there is no attempt to flatten the demand curve by distributing accepts among geographically separated resources of the same legal entity (e.g. apparel store chain). We will extend the algorithm to implement load balancing at a later stage.
 
3. Note that for campus settings, where the resources are classrooms, although they are geographically separated, they are part of a campus and we need to account for admissions across such resources, to enable actors to be admitted into as many resources as it is possible and fair for the day. This is not conflicting with (2) where the actor extracts the same utility if she is admitted to the specific store or the other nearby. 

4. There is no semantic consideration of the host type in the decision making algorithm. For example, we do not consider special circumstances such as theaters and other sports venues as they control the reservations and seating on their own to maintain social distancing. These hosts are usually not dealing with sequential decision processes in the sense that actors arriving for each event and they are not expected to arrive for the same event in the future. 
   
5. There is no dynamic tracking of changing density of actors within the resource. This is important for large resources such as office buildings or campuses where social distancing can be maintained for some resources (e.g classrooms) but not in the same way as others e.g. cafeterias / common spaces. The system will be extended via video surveillance and other actor localization / counting technologies, to consider actor mobility and congestion events from people dont adhering to social distancing guidelines. 

6. The system must be fair. If one sends multiple reservations requests one after the other to the system for a resource, the decision maker must be able to detect such attempts to game the system and fairly assign the resources across time. 

7. There are no risk (also known as actor cost) considerations in the decision making process. An actor that requests a reservation that lives far away and travels via public transportation (higher risk of infecting others) has equal chances to another that lives next to the requested address (lower risk). Similarly, an actor that requests multiple reservations during the day posses greater risk to another that doesn't. For example a commuting student that reserves multiple resources e.g. corresponding to different classes throughout the day. This is a simplifying assumption for now that will be revisited in the future to account for actor risk(s). 
