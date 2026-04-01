INPUT CODE

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Employee {
private:
    int id;
    string name;
    float salary;

public:
    void read(ifstream &fin) {
        fin >> id >> name >> salary;
    }

    void calculateSalary() {
        float bonus = 0.1 * salary;   // 10% bonus
        float deduction = 0.05 * salary; // 5% deduction
        salary = salary + bonus - deduction;
    }

    void write(ofstream &fout) {
        fout << id << " " << name << " " << salary << endl;
    }

    void display() {
        cout << id << " " << name << " " << salary << endl;
    }
};

int main() {
    ifstream fin("input.txt");
    ofstream fout("output.txt");

    if (!fin || !fout) {
        cout << "File error!" << endl;
        return 1;
    }

    Employee e;

    cout << "Updated Records:\n";
    while (fin) {
        e.read(fin);
        if (fin) {
            e.calculateSalary();
            e.write(fout);
            e.display();
        }
    }

    fin.close();
    fout.close();
    return 0;
}
```


OUTPUT
data provided 
101 Amit 20000
102 Riya 30000
103 Rahul 25000


final output 
101 Amit 20000
102 Riya 30000
103 Rahul 25000
