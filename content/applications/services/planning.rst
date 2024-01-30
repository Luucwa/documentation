:show-content:

========
Planning
========

**Odoo Planning** is a flexible tool that allows you to plan your team's schedule and manage shifts
and resources.

Handling your team's planning comes with specific requirements that may vary widely depending on
your business needs. Several concepts were introduced in Odoo Planning to meet those needs.

Shifts are dispatched to resources, which can be either :ref:`human <planning/employees>`
(employees) or :ref:`material <planning/materials>` (e.g., equipment). The resources are assigned
:ref:`roles <planning/roles>`, which allows for streamlining the work within the team.

Once the initial configuration is done, :ref:`planning shifts <planning/shifts>` can be done
manually or automated by using the :ref:`auto planning <planning/open-shifts>` feature.

An integration between the Planning and Sales apps has been introduced, allowing the linking of sold
services to roles and shifts in Planning. Additionally, integration with Project allows dedicating
shifts, and thus time and resources, to specific projects.

.. seealso::
   - `Planning tutorials <https://www.odoo.com/slides/planning-60>`_

.. _planning/configuration:

Configuration
=============

.. _planning/roles:

Roles
-----

To define the roles your resources perform (e.g., chef, bartender, waiter), go to
:menuselection:`Configuration --> Roles --> New`, then fill in the Name (e.g., assistant,
receptionist, manager).

Then, choose the **Resources** that will perform this role. Resources can be either
:ref:`Employees <planning/employees>` or :ref:`Materials <planning/materials>`.

.. note::
   - If the Sales app is installed in your database, an additional field appears, allowing you to
     specify which roles are needed to perform services so that the shifts are dispatched to the
     right person.
   - Roles are taken into account when using the :ref:`Auto Plan feature <planning/open-shifts>`.

Property fields and roles
~~~~~~~~~~~~~~~~~~~~~~~~~

**Property fields** allow you to add custom fields to forms across several Odoo applications.
Planning includes the possibility of adding property fields linked to roles to shifts.

To create a property field, open Planning, then switch to :guilabel:`List view`. From there, click
:guilabel:`View` on the shift that you wish to edit. If the :guilabel:`Role` field is empty, fill it
in with the desired role, then press the cog icon and click :guilabel:`Add Properties`. `Configure
<https://www.odoo.com/documentation/17.0/applications/productivity/knowledge/properties.html>`_ the
new field according to your needs.

.. image:: planning/add-properties.png
   :alt: Creating a new property field in Planning.

The property field is linked to the role and is included in the shift form of all shifts performed
by this role.

.. example::
   Some of the use cases of role property fields include:

   - **Accreditation**: for roles that require a specific permit (e.g., driving license)
   - **Location**: in companies that operate in multiple locations (e.g., shops or restaurants)
   - **Language**: in a multi-lingual environment (e.g., consulting company)

.. _planning/employees:

Employees
---------

All employees can be included in the planning and have shifts assigned to them.

To adapt the employee's planning settings, go to :menuselection:`Planning --> Configuration -->
Employees`, and choose the employee for whom you want to edit the settings. Then, go to the
:guilabel:`Work Information` tab.

.. tip::
   You can do the same by opening the **Employees** app from your dashboard.

.. note::
   **Odoo Employee** is installed by default along with Planning.

Two sections of the employee's :guilabel:`Work Information` tab have an impact on Planning:
:guilabel:`Schedule` (namely, the :guilabel:`Working hours` option) and :guilabel:`Planning`.

.. image:: planning/employee.png
   :alt: Work information tab on the user's profile.

Working hours
~~~~~~~~~~~~~

The **working hours** are taken into account when the :guilabel:`Allocated Time` and its percentage
is calculated for :ref:`shifts <planning/templates>`. If the working hours field is left blank, the
employee is considered to be working flexible hours.

You can also create individual :guilabel:`Working Times` (for example, for employees working
part-time), by clicking :guilabel:`Search more...`, then  :guilabel:`New`.

.. note::
   The Working Times and time allocated in Planning can impact **Payroll**, if your contract is
   configured to generate work entries based on shits.

.. seealso::
   - `Payroll documentation <https://www.odoo.com/documentation/17.0/applications/hr/payroll.html>`_

Planning roles
~~~~~~~~~~~~~~

Once an employee has one or more :guilabel:`Planning roles`:

- When creating a shift for this employee, only the shift templates from the roles chosen in this
  field will be displayed.
- When a schedule is published, the employee will only be notified of open shifts for the roles that
  are assigned to them.
- When auto-assigning open shifts or planning sales orders, the employee will only be assigned
  shifts for the roles assigned to them.

Additionally, when a :guilabel:`Default role` is defined:

- When creating a shift for the employee, the default role will be automatically selected.
- This role will also have precedence over the other roles of the employee when auto-assigning open
  shifts or planning sales orders.

.. note::
   If the Planning roles fields are left empty, there are no restrictions in the shift templates and
   open shifts shared with the employee. However, it’s not possible to use the **Auto Plan** feature
   for employee with no roles.

.. _planning/materials:

Materials
---------

**Materials** are resources that can be assigned shifts and working hours but are not employees.
For example, a construction company could use Materials to create shifts for shared machines
(e.g., cranes, forklifts).

Similarly to Employees, Materials can be assigned Roles, Default Role, and Working Time.

.. _planning/templates:

Shift Templates
---------------

To create a shift template, open any existing shift, then tick :guilabel:`Save as template`.

Alternatively, you can go to :menuselection:`Configuration --> Shift Templates`, then press
:guilabel:`New`. Fill in the :guilabel:`Start Hour` and :guilabel:`Shift Duration`. The shift’s
:guilabel:`End Time` is then calculated based on the :guilabel:`Company working hours`, taking into
account working time as well as breaks.

.. example::
   The Company Working Hours are Monday to Friday, 8 am to 5 pm, with a break between 12 and 1 pm.

   - Creating a Shift Template with a Start Hour of 9 am and a duration of 8 hours will result in
     the End Hour being 5 pm, based on the Company Working hours and the 1-hour break.
   - Creating a Shift Template with a Start Hour of 10 am and a duration of 10 hours will result in
     the End Hour of 10 am the following day, as the Company is closed at 5 pm according to Company
     Working Hours.

Additionally, for each shift template, you can also configure:

- :guilabel:`Role` - This shift will be linked to this specific role only.
- :guilabel:`Project` - Selecting a project allows you to keep track of shifts that are dedicated to
  work on the project.

.. _planning/shifts:

Planning shifts
===============

On opening the Planning app, the planning view shows the users their own shifts. Users with admin
roles can also see :guilabel:`Schedule by Resource`, :guilabel:`Role`, :guilabel:`Project`, or
:guilabel:`Sales Order`, as well as reporting and configuration menus.

The overview is displayed in the Gantt view, which allows you to edit the shifts with a drag and
drop, resize, split, and duplicate without having to open the individual shift.

.. image:: planning/overview.png
   :alt: A schedule displaying varius visual elements.

The following visual elements are used on the shifts in the Planning overview:

- **Full color**: shifts that are planned and published.
- **Diagonal stripes**: shifts that are planned but have not yet been published.
- **Grayed-out background**: employees that are on time off.
- **Progress bar**: shifts that are currently ongoing and have timesheets linked to them.
- **Grayed-out shift**: when copying shifts, the copied shifts are shown in full color, whereas
  previously existing shifts are temporarily greyed out. The color changes back to full color or
  diagonal stripes on the next refresh of the page or by removing the filter.

.. _planning/create-shift:

Create a shift
--------------

To create a shift, click :guilabel:`New`. A window pops up, and the following details can be filled
in:

- :guilabel:`Templates`: if there is one or more templates existing in your database, they are
  displayed in the upper section of the pop-up window. Once selected, a template prefills the
  shift form accordingly.
- :guilabel:`Resources`: resources can be both employees or materials. If this field is left empty,
  the shift is considered an :ref:`open shift <planning/open-shifts>`.
- :guilabel:`Role`: select the role that the resource assigned will be performing. This field is
  used when :ref:`auto-planning <planning/open-shifts>` shifts. Once you select a role, the shift
  templates associated with it are displayed in the upper section of the pop-up window.
- :guilabel:`Project`: if Project app is installed in your database, a field allowing you to link
  the project to the shift is available, allowing you to plan and track shifts dedicated to work on
  the selected project.
- :guilabel:`Sales Order Item`: if Sales app is installed in your database, a field allowing you to
  link a Sales Order to the shift is available.
- :guilabel:`Repeat`: tick the checkbox and configure the :guilabel:`Repeat Every` field according
  to your needs. The following rules apply to recurring shifts:

  - All fields (e.g. :guilabel:`Resource`, :guilabel:`Role`, :guilabel:`Project`) are copied from
    the original shift except for the date, which is adjusted according to the
    :guilabel:`Repeat Every` field.
  - Recurrences are planned but not published.
  - By default, planned shifts are created six months in advance, after which they are created
    gradually. To change the time frame, go to :menuselection:`Configuration --> Settings -->
    Recurring shifts`.

- :guilabel:`Save as Template`: when this option is ticked, a shift template is created with the
  same :guilabel:`Start and End hours`, :guilabel:`Allocated time`, :guilabel:`Role`,
  and :guilabel:`Project`.
- :guilabel:`Note`: additional note that is sent to the employee on shift publishing.
- :guilabel:`Date`: choose the date and time of your shift. This is the only mandatory field when
  creating a shift.
- :guilabel:`Allocated time`: is calculated based on the date and the employee’s :guilabel:`Working
  Schedule`. See more in :ref:`Shift Templates <planning/templates>`.

Press :guilabel:`Publish & Save` to confirm the shift, and send the assigned employee their schedule
by email.

.. note::
   The draft is visible on the admin planning view and can be identified by diagonal lines. The
   employee is only notified of the shift once it's published.

   Two kinds of notifications are sent to the employees depending on their account configuration:

   - Employees without user accounts are redirected to a dedicated Planning portal.
   - Employees with a user account are redirected to the back end of Odoo.

.. _planning/open-shifts:

Open shifts and auto planning
-----------------------------

The :guilabel:`Auto Plan` button allows you to assign **Open shifts** (shifts with no resource
assigned) and create and assign shifts linked to Sales Orders or Project.

The following features have an impact on auto planning:

- **Roles**: open shifts are only assigned to resources (employees or materials) that have the
  corresponding role assigned.
- **Default roles**: the default role assigned to a resource is given priority over the other roles
  they have assigned to them.
- **Conflicts**: employees or materials cannot be assigned multiple shifts at the same time.
- **Time off**: the employees’ time off is taken into account, as well as public holidays.
- **Company working hours**: are taken into account when assigning shifts to employees or materials.
- **Contracts**: employees without an active contract cannot be assigned shifts.

Press :guilabel:`Publish` to confirm the schedule and notify the employees of their planning.

.. _planning/switching-unassignment:

Switching shifts and unassignment
---------------------------------

Two features are available to allow employees to make changes to their schedule:
**switching shifts** and **unassignment**.

.. note::
   These features are mutually exclusive. Switching shifts is possible by default and cannot be
   disabled. However, once the **Allow unassignment** feature is enabled, it replaces the option to
   switch shifts.

Switching shifts
~~~~~~~~~~~~~~~~

If an employee then wishes to switch a shift, they can click the unwanted shift and click
:guilabel:`Ask to switch`.

The shift remains assigned to the original employee, but in the shift overview, a notification
informing that the assigned employee would like to switch shifts is visible on the shift.

The shift is then displayed to other employees who share the same role, and if they wish to assign
it to themselves, they click the :guilabel:`I take it` button.

The following rules apply:

- The :guilabel:`ask to switch` button is only visible to users with the user access right.
- Only the shifts matching the employee's roles are displayed as available to them.
- Switching shifts is only available for shifts that are in the future.

Unassignment
~~~~~~~~~~~~

To allow employees to unassign themselves from shifts, go to
:menuselection:`Configuration --> Settings`, then tick the checkbox :guilabel:`Allow Unassignment`.
Then, specify the maximum number of days that the employees can unassign themselves before the
shift.

Once shifts are planned and published, employees receive an email notification. If shift
unassignment is allowed, the employees can click the :guilabel:`I am unavailable` button, and the
shift reverts to an open shift.

The following rules apply:

- The :guilabel:`Unassign` button is only visible to users with the user access right.
- Only the shifts matching the employee's roles are displayed in their schedule.
- Switching shifts is only available for shifts that are in the future.

