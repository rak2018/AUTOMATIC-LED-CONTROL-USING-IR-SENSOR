# AUTOMATIC-LED-CONTROL-USING-IR-SENSOR
##  AIM
To design and implement a system using the **STM32 microcontroller** where an LED automatically turns ON or OFF based on the input from an **IR sensor**.

---

##  Components Required
- STM32 Nucleo or Discovery Board (e.g., **Nucleo-G071RB**)
- IR Sensor Module
- LED (5mm Green or any color)
- Jumper wires
- Breadboard

---

##  Theory
An **IR sensor** detects the presence of an object by emitting and receiving infrared light.

### IR Sensor Behavior
- When an **object is detected**, the IR sensor output goes **LOW (0V)**.
- When **no object is detected**, the output stays **HIGH (3.3V)**.

### Microcontroller Response
- If **IR output = LOW** → **LED ON**
- If **IR output = HIGH** → **LED OFF**
### **Procedure**

1. Open **STM32CubeIDE**.
<img width="1920" height="1200" alt="Screenshot 2025-11-10 124822" src="https://github.com/user-attachments/assets/7e5ca91d-71c4-4374-bd3e-8bc2d15412d8" />

2. Click **File → New STM32 Project**.
<img width="997" height="558" alt="Screenshot 2025-11-11 043012" src="https://github.com/user-attachments/assets/931f0759-0521-445d-96e0-00ea158e91ec" />
<img width="1037" height="583" alt="Screenshot 2025-11-11 043029" src="https://github.com/user-attachments/assets/59d6c4ca-bc3b-458a-91ef-9b653f07a89c" />

3. Select the **target microcontroller** or board and click **Next**.
<img width="990" height="515" alt="Screenshot 2025-11-11 043101" src="https://github.com/user-attachments/assets/60fc7892-b49a-468c-80a7-51d198403c44" />



4. Name the project.
<img width="655" height="723" alt="Screenshot 2025-11-11 043151" src="https://github.com/user-attachments/assets/bcee9783-bb5c-45f0-9fb4-4894cff368c3" />

5. The corresponding `.ioc` file will be generated automatically.
 <img width="1030" height="594" alt="Screenshot 2025-11-11 043206" src="https://github.com/user-attachments/assets/42cc26b4-1c06-4cba-9c3f-a12bbadae550" />
 
6. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
<img width="997" height="559" alt="Screenshot 2025-11-11 043301" src="https://github.com/user-attachments/assets/6e34cc34-3d0a-4c71-aefa-e7e047932a3f" />
<img width="1030" height="576" alt="Screenshot 2025-11-11 043318" src="https://github.com/user-attachments/assets/d7c7e44c-ffaf-47da-b51b-268eef0d5a4f" />

7. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
<img width="996" height="565" alt="Screenshot 2025-11-11 043337" src="https://github.com/user-attachments/assets/ef0bbaed-3903-40f5-b979-5223fecb4561" />

8. Edit the generated main program as required.
<img width="991" height="553" alt="Screenshot 2025-11-11 043355" src="https://github.com/user-attachments/assets/7ced715a-b231-49d0-afd1-b7ec69f0da8c" />
<img width="1033" height="575" alt="Screenshot 2025-11-11 043416" src="https://github.com/user-attachments/assets/4ff26766-6951-43ae-9f90-450a58585586" />


9. Click **Project → Build All**.
<img width="986" height="566" alt="Screenshot 2025-11-11 043436" src="https://github.com/user-attachments/assets/2e9321e7-1edb-40ca-8427-a6ea77804643" />


10. Link the **HEX file** using the post-build process.
<img width="957" height="439" alt="Screenshot 2025-11-11 043509" src="https://github.com/user-attachments/assets/d9a996fc-b97b-4867-8cd9-1dbfbd0fdd67" />
    
11. Click **Debug** and connect the **STM Nucleo Board**.
 <img width="997" height="556" alt="Screenshot 2025-11-11 043551" src="https://github.com/user-attachments/assets/68860f67-da83-48c1-852b-6f9cce62e538" />
   
12. Click **Run** to execute the program.
    
---

### 💻 **Program**


```c
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}
```
---
### OUTPUT
CASE 1: LED ON 

<img width="887" height="526" alt="Screenshot 2025-11-11 043636" src="https://github.com/user-attachments/assets/490d78f1-3b7c-4b25-935b-1c002e87afd6" />

CASE 2: LED OFF

<img width="823" height="527" alt="Screenshot 2025-11-11 043657" src="https://github.com/user-attachments/assets/92bf8c9b-4e1e-4653-8f08-51521ac19bfb" />

---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.




