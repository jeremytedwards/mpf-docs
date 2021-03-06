achievement_groups:
===================

*Config file section*

.. versionadded:: 0.32

+----------------------------------------------------------------------------+---------+
| Valid in :doc:`machine config files </config/instructions/machine_config>` | **NO**  |
+----------------------------------------------------------------------------+---------+
| Valid in :doc:`mode config files </config/instructions/mode_config>`       | **YES** |
+----------------------------------------------------------------------------+---------+

The ``achievements_groups:`` section of your config is where you configure
grouping of multiple
:doc:`player-based "achievement" tracking </game_logic/achievements/index>`.

Like most things in MPF configs, the highest-level entries in the
``achievement_groups:`` section of your config are the names of the individual
achievement group, and then indented under each of those are the settings for
that group.

Here's an example achievement_groups section from Brooks & Dunn. (This is
related to the example in the achievements config documentation.)

::

    achievement_groups:
      my_group:
        achievements: world_tour, money_bags, music_awards, jukebox, play_poker
        enable_events: enable_mission_selection
        start_selected_events: shot_lower_vuk_from_playfield_hit
        select_random_achievement_events: rotate_mission_rotator
        events_when_enabled: mission_rotator_ready
        rotate_right_events: sw_toggle
        show_tokens:
          leds:
            l_begin_round
        show_when_enabled: flash

General Settings
----------------

achievements:
~~~~~~~~~~~~~
List of one (or more) values, each is a type: ``string``. Default: ``None``

This is a list of the achievements (from the ``achievements:`` section of your
mode config) that make up this group. The order here defines the order
individual achievements are rotated in via the ``rotate_right_events:`` and/or
``rotate_left_events:`` settings.

show_tokens:
~~~~~~~~~~~~
One or more sub-entries, each in the format of type: ``str``:``str``. Default: ``None``

This is an indented list of key/value pairs for the
:doc:`show tokens </shows/tokens>` that will be sent to the shows that are
played when this achievement changes state.

Note that you can configure ``show_tokens:`` at the group level (here) or the
individual achievement level. That's done for convenience, and in practical use,
you'd just configure the show tokens in one place.

Control Events
--------------

The following settings specify which MPF events cause the achievements in
this group to move to a new state.

enable_events:
~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted, cause the achievements in this group to
switch to their "enabled" states. These events will also cause the
achievements to play the show defined in their ``show_when_enabled:`` setting
and to emit (post) events in their ``events_when_enabled:`` settings.

disable_events:
~~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted, cause the achievements in this group to
switch to their "disabled" states. These events will also cause the
achievements to play the show defined in their ``show_when_disabled:`` setting
and to emit (post) events in their ``events_when_disabled:`` settings.

start_selected_events:
~~~~~~~~~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted, cause any achievements in this group that are
in the "selected" state to switch to their "started" state. (Typically there
would only be a single achievement in the group that's "selected" at any time,
but you could have more than one.

When the individual achievements change from "selected" to "started", they will
play their ``show_when_started:`` shows and post their
``events_when_started:`` events.

select_random_achievement_events:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Events in this list, when posted, will randomly pick on of the available
achievements and change it to its "selected" state. This is useful when a game
is starting and you want one of the avaiable achievements to start in a selected
state. (e.g. pick a random mission to be highlighted.)

The "available" achievements which could be chosed here include achievements
that are one of the following:

* enabled
* selected
* stopped (if the achievement's ``restart_after_stop_possible:`` is true/yes

An example of this would be in Attack From Mars, where the next country is
randomly chosen (selected) after you default the saucer for the previous
country.

If there are no more available events to be selected, then the events in
``events_when_no_more_enabled:`` are posted.

Note that if you want to always select a certain achievement (instead of
randomly picking one), then you can just set that particular achievement's
``select_events:`` entry rather than using this random selecting setting.

rotate_right_events:
~~~~~~~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Causes the states of the available achievements in this group to be rotated
to the right.

This is used to "switch" the current selected achievement. For example, many
games have main achievements you need to complete to get to wizard mode.
Completed achievements have a light that's solid on, available (enabled)
achievements have a light that's off (since they're not yet complete but
available to be played), and the current selected achievement has a light that's
flashing (indicating that it's the next one to be played).

Then when you hit a slingshot or pop bumper, the currently selected (flashing)
achievement changes, but you only want to rotate with other achievements that
are enabled (available but not yet complete).

So if this is the current state:

* Mission 1: completed
* Mission 2: selected
* Mission 3: enabled
* Mission 4: enabled
* Mission 5: enabled

And then one of the ``rotate_right_events:`` is posted (like from a pop bumper
hit), the new list would look like this:

* Mission 1: completed
* Mission 2: enabled
* Mission 3: selected
* Mission 4: enabled
* Mission 5: enabled

Notice that the "selected" state moved from Mission 2 to Mission 3, and the
completed state of Mission 1 did not change.

Even though these are called "rotate" events, what really happens is that when
this rotation occurs, the previously selected achievement changes from
"selected" to "enabled", and the newly selected achievement changes from
"enabled" to "selected". Both achievements will stop their current shows and
play the shows associated with their new states, and both will post the events
associted with their new states.

Note that if you want to select a random achievement instead of the next one
on the list, you can use a ``select_random_achievement_events:`` event instead.

rotate_left_events:
~~~~~~~~~~~~~~~~~~~
One or more sub-entries, either as a list of events, or key/value pairs of
event names and delay times. (See the
:doc:`/config/instructions/device_control_events` documentation for details
on how to enter settings here.

Default: ``None``

Same as ``rotate_right_events:``, but it rotates the selected achievement in the
opposite direction.

Events posted by achievements
-----------------------------

You can configure achievements to post certain events when they change state.

Note that all achievements will always post events in the form
:doc:`/events/achievement_name_state_state` when they change state. The events
listed below are in additional to that event.

events_when_enabled:
~~~~~~~~~~~~~~~~~~~~
List of one (or more) values, each is a type: ``string``. Default: ``None``

A single event, or a list of events, that will be posted when this achievement
group is enabled.

events_when_all_complete:
~~~~~~~~~~~~~~~~~~~~~~~~~
List of one (or more) values, each is a type: ``string``. Default: ``None``

A single event, or a list of events, that will be posted when all the
achievements in this group are in the "completed" state. This is useful for
posting events to start a wizard mode, for example.

events_when_no_more_enabled:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
List of one (or more) values, each is a type: ``string``. Default: ``None``

A single event, or a list of events, that will be posted when one of the events
in the ``select_random_achievement:`` is posted but there are no more available
achievements to be selected.

Shows
-----

The following settings control which show is played when this achievement
switches to a new state.

Note that whatever show was playing from the previous state will be stopped.

Also, any tokens configured in the ``show_tokens:`` section will be passed to
the show here.

show_when_enabled:
~~~~~~~~~~~~~~~~~~
Single value, type: ``string``. Default: ``None``

Name of the show that will be started when this achievement group has been
enabled.
