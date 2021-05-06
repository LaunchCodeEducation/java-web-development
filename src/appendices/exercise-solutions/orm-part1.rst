.. _orm1-exercise-solutions:

Exercise Solutions: OMG the ORM!
================================

.. _orm1-exercise-solutions-class:

The ``EventCategory`` Class
---------------------------

First, create a new class called ``EventCategory`` in the ``models`` directory.

``EventCategory`` needs to have the following:

#. An ``id`` field of type ``int``.
#. A ``name`` field of type ``String``.
#. A constructor.
#. The appropriate getters and setters.

``EventCategory`` represents data that will be stored in our database, so you need to use the ``@Entity`` annotation!

.. sourcecode:: java
   :linenos:

   @Entity
   public class EventCategory {

      @Id
      @GeneratedValue
      private int id;

      @Size(min=3, message="Name must be at least 3 characters long")
      private String name;

      public EventCategory(@Size(min = 3, message = "Name must be at least 3 characters long") String name) {
         this.name = name;
      }

      public EventCategory() {}

      public String getName() {
         return name;
      }

      public void setName(String name) {
         this.name = name;
      }

      public int getId() {
         return id;
      }

      @Override
      public String toString() {
         return name;
      }

      @Override
      public boolean equals(Object o) {
         if (this == o) return true;
         if (o == null || getClass() != o.getClass()) return false;
         EventCategory that = (EventCategory) o;
         return id == that.id;
      }

      @Override
      public int hashCode() {
         return Objects.hash(id);
      }
   }

:ref:`Back to the exercises <orm1-exercises>`

.. _orm1-exercise-solutions-methods1:

The ``EventCategoryController`` Class
-------------------------------------

``displayAllEvents``
^^^^^^^^^^^^^^^^^^^^

``displayAllEvents`` needs to do the following:

#. Use ``@GetMapping`` and return ``"eventCategories/index"``.
#. Add an attribute for the ``title`` that uses ``"All Categories"``.
#. Add an attribute for the ``categories`` that uses all of the values in your ``EventCategoryRepository`` variable.

.. sourcecode:: java
   :linenos:

   @GetMapping
   public String displayAllCategories(Model model) {
      model.addAttribute("title", "All Categories");
      model.addAttribute("categories", eventCategoryRepository.findAll());
      return "eventCategories/index";
   }

:ref:`Back to the exercises <orm1-exercises>`

.. _orm1-exercise-solutions-methods3:

``processCreateEventCategoryForm``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``processCreateEventCategoryForm`` needs to do the following:

#. Use ``@PostMapping``.
#. Use error validation and the ``Errors`` object appropriately. If you want to review how to use the ``Errors`` object, check out the section on :ref:`error validation <validating-models>`.
#. Add an attribute for the ``title`` and assign it ``"Create Category"``.
#. Add an attribute for a new instance of ``EventCategory``.
#. Either return ``"eventCategories/create"`` or ``"redirect:"``.

.. sourcecode:: java
   :linenos:

   @PostMapping("create")
   public String processCreateEventCategoryForm(@Valid @ModelAttribute EventCategory eventCategory, Errors errors, Model model) {

      if (errors.hasErrors()) {
         model.addAttribute("title", "Create Category");
         model.addAttribute(new EventCategory());
         return "eventCategories/create";
      }

      eventCategoryRepository.save(eventCategory);
      return "redirect:";
   }

:ref:`Back to the exercises <orm1-exercises>`

.. _orm1-exercise-solutions-templates:

Thymeleaf Templates
-------------------

To finish the exercises, we need to make two new templates.

#. ``eventCategories/index``, which will contain a table of the event categories.

   .. sourcecode:: html
      :linenos:

      <!DOCTYPE html>
         <html lang="en" xmlns:th="http://www.thymeleaf.org/">
            <head th:replace="fragments :: head"></head>
            <body class="container">

               <header th:replace="fragments :: header"></header>

               <table class="table table-striped">
                  <thead>
                  <tr>
                     <th>Category Name</th>
                  </tr>
                  </thead>
                  <tr th:each="category : ${categories}">
                     <td th:text="${category.name}"></td>
                  </tr>

               </table>

            </body>
         </html>

:ref:`Back to the exercises <orm1-exercises>`
