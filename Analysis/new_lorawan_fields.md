# Analysis LoRaWAN Uplink Data Model

[[TOC]]

# Metadata

- Author: schlotkrabbe
- Date: 2025-10-21

# Subject of Analysis

Find out which additional fields are interesting from TTN.

# Scope and Context

based on the TTN communications data, example can be found below.

# Observations

- Timing fields should be excluded, very likely not relevant for us

- gateway metadata should be excluded, very likely not relevant for us

  - network IDs
  - locations

- sometimes multiple gateways get the message, this creates issues with storage, strategy is required, pick strongest?

## Included Fields

### `channel_rssi`

Per-channel RSSI value, limited to the specific RF channel used for the transmission.  
_Reason for inclusion:_ Provides finer diagnostic detail in environments with high interference or multi-channel gateways. It's valuable when correlating signal degradation with specific frequency slots.

### `confirmed`

Boolean indicating whether the uplink requested confirmation from the Network Server.  
_Reason for inclusion:_ Useful for understanding transmission modes and energy consumption trade-offs. Confirmed uplinks consume more airtime and affect duty-cycle performance but guarantee delivery.

### `consumed_airtime → airtime`

Total radio transmission time for this uplink, expressed as a duration (e.g., "0.823296s").  
_Reason for inclusion:_ Airtime directly affects energy consumption, duty-cycle compliance, and spectrum utilization.

### `data_rate.lora.spreading_factor`

LoRa parameter defining symbol duration and range. Higher SF means longer range but slower transmission.  
_Reason for inclusion:_ One of the most critical metrics for network optimization. It determines effective data rate, device energy use, and gateway load. Tracking SF allows adaptive data rate (ADR) analysis.

### `data_rate.lora.coding_rate`

Forward Error Correction ratio (e.g., "4/5", "4/7").  
_Reason for inclusion:_ Indicates redundancy level in the modulation. Helps explain packet success rates and resilience to interference. Essential for advanced RF performance metrics.

### `f_cnt`

The frame counter from the device, incremented for each uplink.  
_Reason for inclusion:_ Core metric for packet loss detection and session continuity. Gaps or resets indicate lost frames or device rejoins.

### `frequency`

Transmission frequency in Hz.  
_Reason for inclusion:_ Required to map channel usage, detect congestion, and enforce regulatory compliance in the 868 MHz band. Frequency distribution statistics help identify hotspots and hardware misconfiguration.

### `frm_payload → original payload`

The Base64-encoded LoRaWAN payload before decoding.  
_Reason for inclusion:_ Preserving the raw payload allows for decoder reprocessing if parsing logic changes or new sensor firmware introduces modified formats.

### `rssi`

Received Signal Strength Indicator in dBm. Reflects the total signal power measured at the gateway's radio front-end during reception.  
_Reason for inclusion:_ RSSI is a fundamental indicator of link budget quality. Tracking it across time allows identification of weak coverage areas and early detection of fading or interference.

### `snr`

Signal-to-Noise Ratio in decibels. Indicates how clearly the signal was distinguishable from background noise.  
_Reason for inclusion:_ SNR directly determines whether packets can be demodulated successfully at a given spreading factor. It supports evaluation of environmental noise and gateway placement quality.

---

## ❌ Excluded Fields

### `ApplicationUp` (container type)

High-level message wrapper from TTN.  
_Reason for exclusion:_ Structural metadata only, no analytical value once parsed.

### `channel_index`

Gateway channel number (0–7).  
_Reason for exclusion:_ Strictly hardware-specific; relevant only for gateway-level debugging.

### `data_rate.lora.bandwidth`

RF bandwidth in Hz.  
_Reason for exclusion:_ While technically dynamic, it provides little analytical value when spreading factor and frequency are already tracked. Variations are typically fixed within band plans.

### `f_port`

Application port that indicates which decoder to use.  
_Reason for exclusion:_ Separator for different payloads, not required by project

### `location.{latitude, longitude, altitude, source}`

Geographic position and elevation of the gateway receiving the packet.  
_Reason for exclusion:_ irrelevant for app users like us

### `received_at` (gateway level)

Timestamp when the gateway server received the frame.  
_Reason for exclusion:_ Redundant with the stored network timestamp; adds no analytical differentiation.

### `time`

Gateway GPS timestamp of reception.  
_Reason for exclusion:_ Only relevant for advanced timing diagnostics (TDoA). Gateway-level debugging not required in this context. See timing chapter

### `timestamp`

SX130x chip counter (microseconds since PPS).  
_Reason for exclusion:_ Used for fine-grained timing correlation; adds no business or analytical insight. see timing chapter

# Supporting Data

## Sample Payload

[new_lorawan_fields-sample.json](new_lorawan_fields-sample.json)
