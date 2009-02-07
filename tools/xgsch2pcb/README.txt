=============================
xgsch2pcb - a GUI for gsch2pcb
==============================


Introduction
------------

When designing a printed circuit board (PCB) it's often desirable to
create a 'schematic' which shows the components to be used and their
connectivity in an abstract fashion.  The connectivity information is
then used to help when designing the actual circuit board.

``gsch2pcb`` is a command-line tool, part of the gEDA suite, which is used
to generate and update a PCB layout.  It works with schematics created
by ``gschem``, part of the gEDA suite, and layouts created by ``pcb``, a
PCB layout system commonly used with gEDA.

``xgsch2pcb`` provides an intuitive, user-friendly graphical interface to
``gsch2pcb``.


Requirements
------------

``xgsch2pcb`` requires:

 * python >= 2.4
 * python-gtk2 >= 2.8
 * python-gobject (if using python-gtk2 >= 2.10)
 * python-dbus
 * A recent version of the gEDA suite
 * A version of ``pcb`` compiled with D-Bus support.

Optionally:
 * python-gnome2 (For launching the about URL)

Building ``xgsch2pcb`` from source code additionally requires:

 * autoconf >= 2.59
 * automake


Installation
------------

If you have fetched the sources from the git repository you will need to
create the necessary autoconf files. To do this, change into the source
directory and execute the command:

autoreconf

This generates a ./configure script amongst other things, which you can run
to configure the software.

As long as you have all the dependencies installed:

  ./configure && make install


Usage
-----

  xgsch2pcb [project]

The main window is divided into three main areas:

* The toolbar at the top offers the usual options to quit the
  program and to load and save project files.

* The left hand 'Schematic' frame shows a list of schematic pages that
  the PCB layout will be based on. The 'Edit schematic' and 'Edit
  attributes' buttons respectively launch ``gschem`` and ``gattrib`` to
  edit the selected schematic page.

* The right hand 'Layout' pane shows the name of the PCB layout file
  associated with the project. The 'Edit layout' button launches
  ``pcb`` to edit a file, and will offer to update your PCB layout if
  necessary.  The 'Update layout' button forces an update of the PCB
  layout even if one isn't strictly necessary.

In order for the update process to work properly, you should never
launch ``pcb`` to edit your PCB layout except through ``xgsch2pcb``.
If you are editing the layout without ``xgsch2pcb`` running and then
wish to edit your layout you should close ``pcb``, launch
``xgsch2pcb`` and then use the 'Edit layout' button to launch ``pcb``
again.

The update process will carry out the following actions to modify your
layout, after launching ``pcb`` if isn't already running:

1. Remove any elements from the layout that are not in the schematic.

2. Find any elements that are in the schematic but not in the layout,
   and add them to the layout (in the top left corner). N.b. that it's
   probably a good idea to leave this corner of your layout clear
   until the layout is more or less finalised, to avoid new elements
   interfering with elements which have already been placed and
   routed.

3. Clear your rats and load a new rats nest.

4. Update the component pin names to match the pin names on the
   schematic symbol.

Note that the update process won't modify your PCB file on disk, and 
will take into account any changes you have made since you last 
saved.

