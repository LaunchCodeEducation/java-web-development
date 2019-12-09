.. _models_in_MVC:

Models and Model Binding
========================

.. toctree::
   :maxdepth: 3

   intro
   model-intro
   update-work
   model-binding
   binding-practice
   exercises
   studio

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



