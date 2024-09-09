# ESP-Home-RF-FOB

YAML code for ESP-Home to Transmit & Receive 433Mhz Key Fob Data.

I wrote this small code to program custom FOB data into a few cheap Ebay FOBS



remote_transmitter:
  pin: 
    number: GPIO14
    mode: INPUT
    inverted: False
  carrier_duty_percent: 100%
  rmt_channel: 4
  
switch:
  - platform: template
    name: "RF FOB Button A"
    turn_on_action:
      - remote_transmitter.transmit_rc_switch_raw:
          code: '110010100100000100110001'
          protocol: 1
          repeat:
            times: 50
            wait_time: 0ms

  - platform: template
    name: "RF FOB Button B"
    turn_on_action:
      - remote_transmitter.transmit_rc_switch_raw:
          code: '110010100100000100110010'
          protocol: 1
          repeat:
            times: 50
            wait_time: 0ms

  - platform: template
    name: "RF FOB Button C"
    turn_on_action:
      - remote_transmitter.transmit_rc_switch_raw:
          code: '110010100100000100110011'
          protocol: 1
          repeat:
            times: 50
            wait_time: 0ms

  - platform: template
    name: "RF FOB Button D"
    turn_on_action:
      - remote_transmitter.transmit_rc_switch_raw:
          code: '110010100100000100110100'
          protocol: 1
          repeat:
            times: 50
            wait_time: 0ms






remote_receiver:
  pin: 
    number: GPIO9
    mode: INPUT
    inverted: True
  dump:
    - rc_switch #Decode and dump RCSwitch RF codes.
  tolerance: 60% 
  filter: 250us
  idle: 4ms
  buffer_size: 16kb
  rmt_channel: 4

binary_sensor:
  - platform: remote_receiver
    name: RF Button Keyfob1A
    rc_switch_raw:
      protocol: 6
      code: '110010100100000100110001'
    filters:
      - delayed_off: 100ms

  - platform: remote_receiver
    name: RF Button Keyfob1B
    rc_switch_raw:
      protocol: 6
      code: '110010100100000100110010'
    filters:
      - delayed_off: 100ms

  - platform: remote_receiver
    name: RF Button Keyfob1C
    rc_switch_raw:
      protocol: 6
      code: '110010100100000100110011'
    filters:
      - delayed_off: 100ms

  - platform: remote_receiver
    name: RF Button Keyfob1D
    rc_switch_raw:
      protocol: 6
      code: '110010100100000100110100'
    filters:
      - delayed_off: 100ms        
