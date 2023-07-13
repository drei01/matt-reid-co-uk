---
layout: post
title: Domain Driven Design in reality
canonical_url: https://tech.small-improvements.com/implementing-domain-driven-design-at-small-improvements/
---

<img src="https://tech.small-improvements.com/wp-content/uploads/2019/05/domain-driven-design-small-improvements-1000x667.jpg" alt="" height="485" width="667">

<iframe sandbox="allow-scripts" scrolling="no" height="250" width="667" data-appid="dbtLvB_w7" class="app-ep-iframe" frameborder="0" src="https://play.ht/embed/?article_url=https://www.matt-reid.co.uk/2019/07/24/domain-driven-design-in-reality.html&voice=en-GB-Wavenet-D" article-url="https://www.matt-reid.co.uk/2019/07/24/domain-driven-design-in-reality.html" allowfullscreen=""></iframe>

We all love reading about the latest software developments trends and buzzwords but they can often turn out to be just that, buzzwords. For us at Small Improvements, Domain Driven Design (DDD) has really lived up to it’s own hype though and helped us build better software, faster and fewer bugs to boot. Do we have any evidence to back up that claim you ask? Well, here’s an example taken from one of our features 1:1 Meetings and how DDD helped us turn the codebase from a jungle of hidden traps, into a joyous place to be.

## The old architecture

Two years ago, our 1:1 Meetings feature was structured as you’d expect with a traditional OO web application, we had three basic layers:

* **Data Access** (DAO) – Meeting, Meeting Space (represents all the meetings between two people), Meeting Content (talking points for a meeting)
* **Service** – A service for each DAO object
* **API** – An endpoint for each object

API requests from the frontend hit the API layer, which in turn invoked a service method to say, create a new meeting. The service method would create a new database entity and invoke the DAO layer to save it to the database. The saved entity would then be converted to a DTO (Data Transfer Object) to pass back to the frontend. Nothing so strange there but as the feature got more complicated we started seeing a few problems arise.

Meetings and their content are stored separately in the database, we had API endpoints to interact with them separately (one or more users can be working on the talking points of the same meeting). We wanted to send all the data about a meeting back to the frontend so we ended up with DTO’s like MeetingWithContent. Then we needed both the meeting and it’s content with a service method so we started passing the MeetingWithContent object into the service layer. Sometimes a service would end up with the wrong object (it needed the database entity instead of the DTO) so would have to convert between them. In general this made the code very hard to read and the separation between the Domain, Database entities and the View layer was very ambiguous.

After reading about DDD, we decided to embark on a refactoring to make the 1:1 Meeting codebase easier to read and extend in the future. We set out our objective:

**Rewrite the 1:1 Meeting domain to separate the layers and make the dependencies and business logic clearer to see.**

## Defining the ubiquitous language

The [ubiquitous language](https://martinfowler.com/bliki/UbiquitousLanguage.html) is a key principle of DDD. The idea is to find a common language for use by everyone involved in the system (from marketing to development, to the user). Once we have a language defined for our application, we can use that to model the architecture. The advantage of defining this common language is that concepts are open and clear to all. There are no cases of “oh but the code doesn’t work like that” from developers or “can we add a new fancy-marketing-term-for-button to the screen?” from marketing. When speaking about the application everyone is on the same page.

In our case we have 1:1 Meetings. Previously, to developers, a 1:1 Meeting was a database entity that contained the participants of the meeting, it’s title etc but not the content of the meeting. A talking point was something that contained a meeting ID (linking back to the meeting database entity). So developers would talk about “saving a talking point” whereas our UI (and customers) would talk about “adding a talking point”. There’s a subtle difference but many of these add up to cause confusion.

We defined our ubiquitous language to talk about meetings in our customer’s (and UI’s) terms. A meeting takes place between two people, each person can add their own talking points to a meeting. They can also add notes, change the date and title of the meeting etc.

## Splitting out layers

DDD defines a layered architecture which starting from the outside (edge of the application that users interact with) only depend on inner layers. None of the layers should depend on any above them. We were clearly violating this principle with our previous architecture and we felt the pain it caused.

<img src="https://tech.small-improvements.com/wp-content/uploads/2019/05/LayersAndDDD-220x300.png" alt="ddd layers" width="460" height="600">

Based on the DDD principles we refactored the code to 4 new layers

* **DAO** (Infrastructure layer): Data access layer
* **Read/Write** (Domain service): Consists of two services
  * Reader – reads an Entity from the DAO and exposes a Meeting domain object.
  * Writer – converts a Meeting domain object to one or more Entities and saves via the DAO layer.
* **Service** (Application service): Consumes and produces Meeting domain objects and “plumbs” together everything required to perform actions on the domain object.
* **API** (Presentation layer): Consumes a actions from HTTP requests, performs those actions using the Application services and converts the resulting domain objects to DTOs

We introduced a new Meeting domain object as an aggregate that is created from database entities and can be converted to a DTO to transfer to the frontend.  This means we no longer have to pass DTO objects around the layers and from the Domain layer upwards we are only dealing with one type of object (a Meeting).

Interaction with our new domain looks like this (pseudo code):

```java
public Meeting addTalkingPoint(String meetingId, String talkingPoint) {
    Meeting meeting = meetingReader.getById(id);
    meeting.addTalkingPoint(talkingPoint);
    meetingWriter.save(meeting);
    return meeting;
}
```

In the background, this creates a new database entity for the talking point and associates it with the meeting in question, but the user doesn’t need to know that as it’s not in the ubiquitous language. The translation and storing of data is hidden away in the DAO layer.

## Why this is better

* We use the ubiquitous language of our domain. A Meeting is something which has two participants. It can be “draft” or not (we never refer to deleted Meetings in the domain layer, they just don’t exist). The actions performed on a Meeting are the same you can perform in the UI (make it visible to certain people, add a talking point, reorder the talking points etc.)
* Business logic (i.e. what gets updated when you share the meeting) is encapsulated within the domain object itself.
* Testing is now easier because all the business logic is in one place (in the domain object).
* Meeting as an Aggregate abstracts away from how the data is stored in the database. We actually store the talking points and the notes separately (and used to have different objects for those), now a consumer only needs to interact with the Meeting object. We could change the way data is stored in the future (e.g. for performance reasons) and we would only need to touch the DAO layer.

The [Aggregate](https://martinfowler.com/bliki/DDD_Aggregate.html) brings other benefits:

* It’s not possible to mutate objects in an invalid way, we always have to go through the Meeting which validates all changes.
* We always have to access our Meeting through the Reader (repository) which forms a natural boundary.\
* We document our ubiquitous language for future developers to discover. The interface of the domain object describes exactly what is possible with a 1:1 Meeting and where to add new functionality.

## We will never be finished

DDD is never “finished”. Our ubiquitous language is constantly evolving and we are always adding new features to our codebase. The work we’ve done enables us to add features faster, new team members can understand the code faster and we have fewer bugs as a result.

*Original article posted on the [Small Improvements tech blog](https://tech.small-improvements.com/implementing-domain-driven-design-at-small-improvements/)*
