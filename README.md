# 🎓 SQL Problem: Students and Examinations

**LeetCode Problem**: [Students and Examinations](https://leetcode.com/problems/students-and-examinations/)

---

## 📄 Problem Description

### Table: `Students`

| Column Name | Type    |
|-------------|---------|
| student_id  | int     |
| student_name| varchar |

- `student_id` is the primary key of this table.
- Each row contains the ID and the name of a student.

---

### Table: `Subjects`

| Column Name | Type    |
|-------------|---------|
| subject_name| varchar |

- `subject_name` is the primary key of this table.
- Each row contains the name of a subject.

---

### Table: `Examinations`

| Column Name  | Type    |
|--------------|---------|
| student_id   | int     |
| subject_name | varchar |

- There is **no primary key** for this table.
- Each row indicates that a student attended an exam in a subject.
- A student can attend the same exam multiple times.

---

## 🎯 Objective

Write an SQL query to **report the number of times each student attended each exam**.

Return the result table **ordered by** `student_id` and `subject_name`.

---

## 🧪 Example

### Input

#### `Students` Table:

| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |

#### `Subjects` Table:

| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

#### `Examinations` Table:

| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Programming  |
| 1          | Physics      |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |

### Output

| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

---

## ✅ SQL Solution

```sql
SELECT 
    s.student_id,
    s.student_name,
    sub.subject_name,
    COUNT(e.subject_name) AS attended_exams
FROM 
    Students s
CROSS JOIN 
    Subjects sub
LEFT JOIN 
    Examinations e 
    ON s.student_id = e.student_id AND sub.subject_name = e.subject_name
GROUP BY 
    s.student_id, s.student_name, sub.subject_name
ORDER BY 
    s.student_id, sub.subject_name;
```

---

## 🧠 Key Concepts

- `CROSS JOIN` to generate all combinations of students and subjects.
- `LEFT JOIN` to bring in actual exam attempts.
- `COUNT()` with `GROUP BY` to tally the number of times each student attended each exam.
- `ORDER BY` to format the output properly.

---

✍️ *Contributed by Deepak Shanmugam K 
📘 *SQL | LeetCode Practice*
