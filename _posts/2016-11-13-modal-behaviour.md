---
layout: post
title:  Modal behaviour 
excerpt: In which modals cause a kerfuffle
---

I've been very lucky to fall into a first front-end role where I'm getting to experience nearly - as far as I can see - all possible permutations of what 'front-end' could be.

I'm simulaneously a web designer, UX engineer, front-end developer and product designer. I've taken my project (I'm the lead, although obviously with help when required!) from a single, standalone screen to a series of single-page apps, and the process has been a fantastic experience so far. I've learned a huge amount and each day can clearly see that I'm doing things that I wouldn't have been able to do when I was first hired, and it's both amazing to look back and see how much better I've become and daunting to realise how much I still have to learn.

I was interested in UX before moving into front end - after all, designing articles for print still requires that you think about how to draw readers in. I've also always been fascinated by how people use things, especially when how they do so isn't necessarily how the thing in question was originally meant to be used. So when my team recently had a rather heated discussion about how modals should behave in a specific circumstance, it was rather interesting to find myself disagreeing with the (eventually) agreed standard.

### A help or a hinderance?
In the app I'm working on, modals are used for all forms - whether it's changing the user's details, updating an address or requesting work, it's in a modal. How the modal should open and close was easy to agree on - after all if you want it open it should open when you click the button that does so, and it should close when you click the button to close it.

When a user clicks on the backdrop, the modal also closes... regardless of how much of the form in question they've filled in. And this is what kicked off the discussion about whether or not consistency in behaviour is more important than silently helping the user.

It's pretty easy to accidently click the backdrop, especially when copying something from a different screen or program that you want to paste into one of the inputs. And it can be hugely frustrating to spend time filling out a form only to lose it because you knocked your mouse the wrong way or accidently clicked where you didn't mean to, and then have to do the whole thing again.

I'm of the opinion that as long as the user hasn't changed or started to fill in the form, clicking the backdrop should absolutely close the modal - but if anything has been changed in the inputs, the user should have to close the modal by clicking on the dedicated button for this purpose. This is not in any way confusing, I feel - the modal can still be easily closed, but if the user has started filling out a form this becomes a conscious decision instead of a potentially accidental occurance. By silently preventing potentially unintended behaviour, the user gets a better experience.

So when I asked my mentor, after spending some time looking up how to achieve the behaviour I wanted, how to accomplish it, I was surprised to kick off an hour-long argument about how modals should behave.

### F*ck off with the confirmations
I should probably mention, briefly, that I detest endless confirmations. The core product of my current company requires the user to confirm that they want to close every modal, side panel or pop-up used in the app, in what I think is a massively frustrating way. Even when the close button is clicked and nothing has been modified, you have to confirm that yes, you do actually want to close the thing that you're trying to close. Because you clicked the close button. Which, to me, sort of implies that you'd like to close the stupid thing.

(I should probably also mention that the users of the core product and the users of the app I'm working on are seperate demographics - users are guaranteed to use one or the other, not both. The two products also appear almost entirely unrelated, design-wise.)

It should come as no surprise, then, that adding in a confirmation that the user would like to close the modal if they (accidently or not) click the backdrop was the first suggestion when I asked my mentor for assistance.

### Consistancy wins
While I'm technically the lead on my project, obviously I'm still very much working under the direction of my manager - which means that consistancy in behaviour won and I've added in a confirmation message inside my modals when the backdrop is accidently clicked, regardless of whether any on the inputs have been filled out or not.

I'm hoping that I'll have time to come back to this and figure out a way to only show the confirmation message when the user has started filling out the form, but it's sadly dropped to the back of my queue as I get on with implementing more of the core functionality that's required.

What's your experience of modals, and how does your company close them? I'd genuinely love to know!


