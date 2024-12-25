# Hospital Management System

The `HospitalManagementSystem` is a Java-based application designed to manage hospital operations, focusing on the `Doctor` module. It provides functionality to view doctors' information and retrieve specific doctor details by ID.

## Features

- **View Doctors:** Display a list of all doctors, including their ID, name, and specialization, in a formatted table.
- **Find Doctor by ID:** Check if a doctor exists in the system using their unique ID.

---

## Prerequisites

To run the system, ensure you have the following:
- Java Development Kit (JDK) 8 or higher
- MySQL Database Server
- A database connection with a table named `doctors` that has the following structure:

```sql
CREATE TABLE doctors (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    specialization VARCHAR(255)
);
```

---

## Installation and Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/opyash218/Hospital_management.git
   cd Hospital_management
   ```

2. **Configure the Database**
   - Update the database credentials in your Java project where the `Connection` object is initialized.

3. **Compile the Code**
   ```bash
   javac HospitalManagementSystem/*.java
   ```

4. **Run the Application**
   ```bash
   java HospitalManagementSystem.Main
   ```

---

## Usage

### **View All Doctors**
Call the `viewDoctors()` method to display a list of all doctors in a tabular format.

### **Find Doctor by ID**
Use the `getDoctorById(int id)` method to check if a doctor with the given ID exists in the database. The method returns:
- `true`: If the doctor exists.
- `false`: If the doctor is not found.

---

## Code Snippet

```java
public void viewDoctors(){
    String query = "select * from doctors";
    try{
        PreparedStatement preparedStatement = connection.prepareStatement(query);
        ResultSet resultSet = preparedStatement.executeQuery();
        System.out.println("Doctors: ");
        System.out.println("+------------+--------------------+------------------+");
        System.out.println("| Doctor Id  | Name               | Specialization   |");
        System.out.println("+------------+--------------------+------------------+");
        while(resultSet.next()){
            int id = resultSet.getInt("id");
            String name = resultSet.getString("name");
            String specialization = resultSet.getString("specialization");
            System.out.printf("| %-10s | %-18s | %-16s |\n", id, name, specialization);
            System.out.println("+------------+--------------------+------------------+");
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
