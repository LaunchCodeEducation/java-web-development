.. _models_in_MVC:

Models and Model Binding
========================

.. toctree::
   :maxdepth: 3

   intro
   model-intro
   bootstrap
   model-class
	model-binding
   binding-practice
   exercises
   studio


## Create Model Class
- Create `models` package 
- Create `Event` class
- Refactor `processCreateEventForm` to create `Event` object
- Refactor `events/index` template to reference `Event` fields
- Test

## Add Class Property
- Add `description` property to class
- Update `events/create` template to include description field
- Update `processCreateEventForm` to create object w/ description 
- Update `events/index` template to display description 

## Add Unique Identifier
- Add `id` property to `Event`
- Add static counter to class
- Update constructor to set `id` 
- Refactor to use no-arg constructor 

## Create Data Layer
- Create `data` package
- Create `EventData` class w/ static members
	- `Map` field to store events
	- `add` method
	- `getById` method
	- `getAll` method w/ `Collection` return type
	- `remove` method 
- Refactor controller to use `EventData` 

## Deleting Events
- Create `renderDeleteEventForm` handler
- Create `events/delete` template w/ form that references IDs
- Create `processDeleteEventForm` handler w/ redirect
- Add link to header fragment 

pojos - plain, console app, nothing inherenet to a spring thing. just an object like we're seen beofre
making distinct objects
move data operations our of the controller
auto create models with model binding

going from hashmap storage to model class

this.name vs. aName - ij generate uses this.notation. meaning the field of the class, not the arg of the constructor

refactor controller to use the model, rather than strings
refactor templates based on changes to controller
thymeleaf - event.name calls the getter behind the scenes

remove does not work before model binding. because it just acts on a string name



