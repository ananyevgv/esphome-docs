basement-controller
========================

.. seo::
    :description: Instructions for setting up a display in ESPHome to show sensor values from Home Assistant
    :keywords: Display

.. figure:: images/dbasement-v2.jpg
    :align: left
    :width: 75.0%

In this example I have used a :doc:`SSD1322 OLED Display over I²C </components/display/ssd1322>` to
show current time and two different temperature values from Home Assistant.


Hardware configuration
----------------------

Hardware is easy! Only four connections are needed:

- ``VCC`` - Power (my display could use either 3.3V or 5V)
- ``GND`` - Ground
- ``SDA`` - Serial Data
- ``SCL`` - Serial Clock

.. warning::

    Ensure your display handles 5V if you use that.

Software configuration
----------------------

Getting Time
************

Get the time from Home Assistant to sync the onboard real-time clock.

.. code-block:: yaml


Getting Temperature
*******************

Next, we want to get two temperature sensors imported from Home Assistant.

I named them ``inside_temperature`` and ``outside_temperature``. You will use those references later.

By adding ``internal: true`` to the sensors they won't be published back to Home Assistant.

.. code-block:: yaml



Define the Fonts
****************

- TrueType fonts are used. If you ever worked with fonts on microcontrollers you will love this!
- Save font files in ``/config/esphome`` folder where your ESPHome configuration is stored.
- The ``.ttf`` suffix must be lowercase and of course match your filename.
- Selection of fonts can be a little bit tricky for small sizes to look good. Experiment and share your findings in the comments below!



Display Definition
******************

Now setup the communication to the display and start fill the screen with live data!

The ``reset_pin`` was not used in my hardware configuration as the display didn't have that pin exposed.

Note your ``address`` and ``model`` might be different, use the scan option to find the address of your display.

.. code-block:: yaml


Rendering
---------

- Alignment of text can use different reference points, for example ``TOP_RIGHT`` or ``BASELINE_LEFT``, which all are defined in :apiref:`display/display_buffer.h`.
- The property ``has_state()`` on a sensor is useful as it can take some seconds to get the data from Home Assistant and you may not want to display ``Nan``
- Refer to the rendering engine :ref:`display-engine` for more features (it can draw lines and circles too!)

Add a Text-Based Sensor
-----------------------

Below follows an example that replaces the "Mitt smarta hem" top printout with the alarm status from the alarm component in Home Assistant.

.. code-block:: yaml




See Also
--------

- :doc:`/components/display/ssd1322`
- :doc:`/components/display/index`
- :doc:`/components/sensor/pulse_counter`
- :doc:`/components/sensor/pulse_meter`
- :doc:`/components/sensor/total_daily_energy`
- :doc:`/components/time/homeassistant`
- :ghedit:`Edit`
