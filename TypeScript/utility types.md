# **Omit**
- generate a new type and provide a type definition
```typescript
interface SoccerPlayer {
    firstName: string;
    lastName: string;
    team: string;
    dob: Date;
    careerGoals: number;
}

//---------------------------
// Omitting single key
//---------------------------
type FreeAgent = Omit<SoccerPlayer,"team">
// create a new type called FreeAgent and removed the "team" properties
const freeSoccerPlayer: FreeAgent {
    firstName: "Paul",
    lastName: "Pogba",
    dob: new Date("15 March, 1993"),
    careerGoals: 28
}

//---------------------------
// Omitting multiple key
//---------------------------
type FreeAgent = Omit<SoccerPlayer,"team" | "careerGoals">
// create a new type called FreeAgent and removed the "team" properties
const freeSoccerPlayer: FreeAgent {
    firstName: "Paul",
    lastName: "Pogba",
    dob: new Date("15 March, 1993"),
}
```
- we can generate a new interface and add new properties different from the properties inherited from another interface with the exception of omitted properties
```typescript
interface FreeAgent extends Omit<SoccerPlayer,"team"> {
    status: string;
}
```

## **When to use Omit?**
### **1. Create "View Models"**
- it is useful to use **omit** type when working with interfaces that interact with different views that don't necessarily require all properties of an object
```typescript
// structure of "Soccer Player" in database
interface SoccerPlayer {
  id: string;
  firtName: string;
  lastName: string;
  team: string;
  dob: Date;
  careerGoals: number;
  dateCreated: Date;
  createdBy: string;
  dateUpdated: Date;
  updatedBy: string;
  isActive: boolean;
}

// consider that we need to generate a form to create a new SoccerPlayer

type RegisterSoccerPlayer = Omit<SoccerPlayer, 'id' | 'dateCreated' | 'createdBy' | 'dateUpdated' | 'updatedBy' | 'isActive'>
```
### **2.Override the property type of existing project**
- What if the SoccerPlayer object data doesn’t match between the UI and the API? 
- For instance, think of fields such as dateCreated or dateUpdated to be strings in the UI, but in the backend they are handle as timestamps or dates.
```typescript
interface SoccerPlayerUI extends Omit<Soccer, 'dateCreated' | 'dateUpdated'> {
  dateCreated: string;
  dateUpdated: string;
}
```