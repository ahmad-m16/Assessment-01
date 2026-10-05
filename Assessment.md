# Software Engineering Intern — Offline Assessment

**Duration:** 120 minutes  **Total marks:** 100  **Mode:** Pen & paper (no internet, no AI tools, no phones)

| Candidate name | Date | Signature |
| -------------- | ---- | --------- |
|                |      |           |

## Instructions

1. Attempt all sections. Section D has a choice.
2. Write code in **JavaScript or TypeScript**. Pseudocode is accepted where noted, but real syntax scores higher.
3. Minor syntax slips are fine. We grade on logic, clarity and edge cases.
4. State any assumptions you make.
5. Keep answers short. A clear 5-line answer beats a vague 20-line one.

| Section | Level        | Topic                                 | Marks | Suggested time |
| ------- | ------------ | ------------------------------------- | ----- | -------------- |
| A       | Basic        | Fundamentals (MCQ + one-liners)       | 20    | 15 min         |
| B       | Basic–Inter. | JavaScript, React, SQL/NoSQL output   | 25    | 30 min         |
| C       | Intermediate | Problem solving / coding              | 30    | 45 min         |
| D       | Advanced     | Design & debugging (choose 1 of 2)    | 25    | 30 min         |

**Context used in the questions:** a small, made-up **clinic appointment system** with patients, doctors, appointments, bills and lab reports. You don't need any healthcare knowledge.

---

## Section A — Fundamentals (20 marks, 1 mark each)

### A1. Multiple choice (circle one)

1. Which HTTP method is most appropriate to **partially update** a patient's phone number?
   (a) GET (b) POST (c) PUT (d) PATCH
2. What does `typeof null` return in JavaScript?
   (a) `"null"` (b) `"object"` (c) `"undefined"` (d) `"number"`
3. Which status code fits "appointment not found"?
   (a) 200 (b) 400 (c) 404 (d) 500
4. `[1, 2, 3].map(x => x * 2)` returns:
   (a) `6` (b) `[2, 4, 6]` (c) `undefined` (d) `[1, 2, 3]`
5. In MongoDB, a collection is most similar to a SQL:
   (a) row (b) column (c) table (d) database
6. Which of these is **not** a JavaScript primitive?
   (a) string (b) symbol (c) array (d) bigint
7. In React, what triggers a component re-render?
   (a) changing a local variable (b) calling `setState` with a new value (c) `console.log` (d) importing a file
8. Which is the safest place to store a database password?
   (a) frontend code (b) Git repo (c) environment variable / secret manager (d) a code comment
9. Time complexity of looking up a key in a JavaScript `Map` (average case):
   (a) O(1) (b) O(log n) (c) O(n) (d) O(n²)
10. `git pull` is roughly equivalent to:
    (a) `git fetch` + `git merge` (b) `git push` + `git fetch` (c) `git clone` (d) `git commit` + `git push`

### A2. One-line answers

11. Difference between `==` and `===`?
12. What is JSON? Give a one-line example of a patient object.
13. What is the difference between `let`, `const` and `var` (one line each)?
14. What does an **index** do in a database, and what does it cost?
15. What is a **primary key**?
16. What is the purpose of a **JWT** in a web app?
17. What does `async`/`await` help with?
18. Name two differences between **SQL** and **NoSQL** databases.
19. What is the difference between **authentication** and **authorization**?
20. What does `npm install` do with `package.json`?

---

## Section B — Read the code (25 marks)

### B1. What is the output? (2 marks each, 10 marks)

```js
// (i)
console.log(1 + "2" + 3);
console.log(1 + 2 + "3");
```

```js
// (ii)
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
```

```js
// (iii)
console.log("A");
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
console.log("D");
```

```js
// (iv)
const patient = { name: "Asha", vitals: { bp: "120/80" } };
const copy = { ...patient };
copy.vitals.bp = "130/90";
console.log(patient.vitals.bp);
```

```js
// (v)
const fees = [500, 300, 200];
const total = fees.reduce((sum, f) => sum + f, 100);
console.log(total);
```

### B2. Find the bug (5 marks)

The function should return the **average fee** of all paid bills. Find every bug and write the corrected version.

```js
function averagePaidFee(bills) {
  let total = 0;
  let count;
  for (let i = 0; i <= bills.length; i++) {
    if (bills[i].status = "PAID") {
      total += bills[i].amount;
      count++;
    }
  }
  return total / count;
}
```

### B3. React (5 marks)

```jsx
function AppointmentCounter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    fetch("/api/appointments/today")
      .then(r => r.json())
      .then(data => setCount(data.length));
  });

  return <p>Today: {count}</p>;
}
```

a) What is wrong with this `useEffect`? What will happen at runtime? (3)
b) Fix it. Also, how would you show a "Loading…" message? (2)

### B4. Queries (5 marks)

Tables (or collections):

- `patients(id, name, phone, city)`
- `appointments(id, patient_id, doctor_id, date, status)` (status is `BOOKED`, `COMPLETED` or `CANCELLED`)

Write a query (SQL **or** MongoDB) for each:

a) All patients from the city "Pune", sorted by name. (1)
b) The number of `COMPLETED` appointments per doctor. (2)
c) Patients who have **never** booked an appointment. (2)

---

## Section C — Problem solving (30 marks)

Write working functions. Mention the time complexity for each.

### C1. Token number formatter (5 marks)

Given a department code and a number, return a token like `OPD-007`. The number is always padded to 3 digits. Numbers above 999 are left as they are.

```
formatToken("OPD", 7)    -> "OPD-007"
formatToken("LAB", 1234) -> "LAB-1234"
```

### C2. Group appointments by doctor (7 marks)

```js
const appts = [
  { id: 1, doctor: "Dr. Rao",  time: "10:30" },
  { id: 2, doctor: "Dr. Iyer", time: "09:00" },
  { id: 3, doctor: "Dr. Rao",  time: "09:15" },
];
```

Return an object that maps each doctor to their appointment ids, **sorted by time**:

```
{ "Dr. Rao": [3, 1], "Dr. Iyer": [2] }
```

### C3. Detect double booking (8 marks)

Each slot is `{ start, end }` in minutes from midnight (for example `570` is 09:30). Write `hasOverlap(slots)` that returns `true` if any two slots for the same doctor overlap. A slot that ends at 600 and one that starts at 600 do **not** overlap.

Bonus (+2, within the 30): do better than O(n²).

### C4. Bill calculator (10 marks)

Write `calculateBill(items, discountPercent)`.

- `items` is a list of `{ name, price, qty, taxPercent }`.
- Line total = `price × qty`, plus tax on that amount.
- Apply the discount to the **pre-tax subtotal only**.
- Round the final amount to 2 decimal places.
- Return `{ subtotal, discount, tax, total }`.
- Throw a clear error for a negative price or qty, or a discount outside 0–100.

Write **3 test cases** you would use to check it, including at least one edge case.

---

## Section D — Design & debugging (25 marks, answer **any one**)

### D1. Design: Online appointment booking API

Design the backend for patients booking doctor appointments.

a) List the **REST endpoints** (method + path + one-line purpose). Include book, cancel, list a doctor's free slots, and list a patient's appointments. (6)
b) Sketch the **data models** (fields and types) for Doctor, Patient, Appointment. (6)
c) Two patients click "Book" for the **same slot** at the same moment. How do you make sure only one succeeds? (6)
d) Patient data is sensitive. List 4 concrete things you would do to protect it (in transit, at rest, in access, in logs). (4)
e) The "list appointments" page is slow with 2 million records. Give 3 things you would check or change. (3)

### D2. Debugging: "The bill PDF shows the wrong patient"

Users report that **sometimes** a printed bill shows another patient's name. It happens mostly at busy hours and can't be reproduced locally. A simplified version of the server code:

```js
let currentPatient = null; // module-level

app.get("/bill/:id/pdf", async (req, res) => {
  const bill = await Bill.findById(req.params.id);
  currentPatient = await Patient.findById(bill.patientId);
  const html = await renderTemplate("bill", { bill });   // takes ~1–2 s
  const pdf = await htmlToPdf(html, { header: currentPatient.name });
  res.type("application/pdf").send(pdf);
});
```

a) Explain the root cause in plain words. Why only at busy hours? (7)
b) Fix the code. (6)
c) There's no check that the logged-in user may see this bill. What's the risk, and how do you fix it? (6)
d) How would you **prove** your fix works, and stop this kind of bug from coming back? Mention logging, tests and code review. (6)

---

## Rough work

&nbsp;

&nbsp;

&nbsp;

---

*End of paper. Check your name is on every sheet before submitting.*
