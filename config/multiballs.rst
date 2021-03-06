multiballs:
===========

*Config file section*

+----------------------------------------------------------------------------+---------+
| Valid in :doc:`machine config files </config/instructions/machine_config>` | **YES** |
+----------------------------------------------------------------------------+---------+
| Valid in :doc:`mode config files </config/instructions/mode_config>`       | **YES** |
+----------------------------------------------------------------------------+---------+

.. overview

The ``multiballs:`` section of your config is where you...

.. todo::
   Add description.

Required settings
-----------------

The following sections are required in the ``multiballs:`` section of your config:

ball_count:
~~~~~~~~~~~
Single value, type: ``integer``.

The number of balls this multiball should eject (and maintain during shoot again period). Note: It may eject more balls when using locks but only ball_count balls will be maintained during shoot again.

Optional settings
-----------------

The following sections are optional in the ``multiballs:`` section of your config. (If you don't include them, the default will be used).

ball_locks:
~~~~~~~~~~~
List of one (or more) values, each is a type: string name of a ``ball_locks:`` device. Default: ``None``

Use those devices first when ejecting balls to the playfield on multiball start. On start all balls from all locks will be ejected (maybe more than ball_count). If there are not enough balls in the lock more balls will be requested to the source_playfield.

debug:
~~~~~~
Single value, type: ``boolean`` (Yes/No or True/False). Default: ``False``

.. todo::
   Add description.

disable_events:
~~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted,

.. todo::
   Add description.

enable_events:
~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted,

.. todo::
   Add description.

label:
~~~~~~
Single value, type: ``string``. Default: ``%``

.. todo::
   Add description.

reset_events:
~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``machine_reset_phase_3, ball_starting``

.. todo::
   Add description.

shoot_again:
~~~~~~~~~~~~
Single value, type: ``time string (ms)`` (:doc:`Instructions for entering time strings) </config/instructions/time_strings>` . Default: ``10s``

.. todo::
   Add description.

source_playfield:
~~~~~~~~~~~~~~~~~
Single value, type: string name of a ``ball_devices:`` device. Default: ``playfield``

.. todo::
   Add description.

start_events:
~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted,
.. todo::
   Add description.

stop_events:
~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted,
.. todo::
   Add description.

tags:
~~~~~
List of one (or more) values, each is a type: ``string``. Default: ``None``

.. todo::
   Add description.

ball_count_type:
~~~~~~~~~~~~~~~~

.. versionadded:: 0.31

single|enum(add,total)|total

TODO
