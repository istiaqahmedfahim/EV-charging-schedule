# Electric Vehicle Scheduling Optimization with Emergency Handling in Charging Station

This repository contains the code for optimizing vehicle schedules to ensure efficient use of charging stations, including handling emergency vehicle entries. The main logic is implemented in the `maincompact.ipynb` file & `emergency_case.ipynb`file, which follows a specific algorithm to prioritize and schedule vehicles.

## Algorithm Overview

1. **Vehicle Differentiation and Selection:**
   - Differentiate and select vehicles for a specific slot.

2. **Filter Vehicles Based on Final SOC:**
   - Drop vehicle schedules where the Final State of Charge (SOC) is below 10%.

3. **Vehicle Classification and Sorting:**
   - Sort the schedules based on vehicle classification (ambulance, fire truck, police, civil).
   - For multiple vehicles within the same class, prioritize those with a lower Final SOC.

4. **Time Requirement Check:**
   - Calculate the total required time for the sorted schedules.
   - If the total time is less than 180 minutes, the schedule is finalized for the slot.
   - Otherwise, follow these steps:
     - Select the lowest priority vehicles in the table with Route 2 and Final SOC above 30%.
     - Drop and add them to a new table for Charging Station 2 until the total required time is below 180 minutes.
     - If the goal is still not met, select and drop the lowest priority vehicles of Route 1 one by one until the total required time is below 180 minutes.

5. **Charging Station 2 Scheduling:**
   - Calculate the total required time from the new table for Charging Station 2.
   - If the total time is less than or equal to the available free time of the same slot at CS2, finalize the schedule.
   - Otherwise, drop vehicle schedules with the maximum Final SOC until the criteria are met.

6. **Handling Emergency Vehicles:**
   - Emergency vehicles can enter at any time by providing the entrance time and charging duration.
   - When an emergency vehicle enters, the onboard vehicle will leave the charging port, splitting its time slot into two portions with the emergency vehicle in the middle.
   - All vehicles below the specific vehicle will be shifted downwards.
   - If the total charging time of slot1 vehicles exceeds 180 minutes due to the emergency vehicle, remove the low-priority vehicles from the list.

*Steps 2-6 are repeated for the vehicle schedules of every time slot from the table of Charging Station 1.*

## Getting Started

### Prerequisites

Ensure you have the following installed:
- Python 3.x
- Jupyter Notebook
- Required Python libraries 

### Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/istiaqahmedfahim/vehicle-scheduling-optimization.git
