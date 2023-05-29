# Query con Select

### Selezionare tutti gli insegnanti
```sql
    SELECT * 
    FROM `teachers`
```

### Selezionare tutti i referenti per ogni dipartimento
```sql
    SELECT `name`, `head_of_department`
    FROM `departments`;
```

### Selezionare tutti gli studenti il cui nome inizia per "E" (373)
```sql
    SELECT * 
    FROM `students`
    WHERE LEFT(`name`, 1)= 'E';
```

### Selezionare tutti gli studenti che si sono iscritti nel 2021 (734)
```sql
    SELECT *
    FROM `students` 
    WHERE YEAR(`enrolment_date`) = 2021;
```

### Selezionare tutti i corsi che non hanno un sito web (676)
```sql
    SELECT * 
    FROM `courses` 
    WHERE `website` is NULL;
```

### Selezionare tutti gli insegnanti che hanno un numero di telefono (50)
```sql
    SELECT * 
    FROM `teachers`
    WHERE `phone`;
```

### Selezionare tutti gli appelli d'esame dei mesi di giugno e luglio 2020 (2634)
```sql
    SELECT * 
    FROM `exams`
    WHERE MONTH(`date`)=06
    OR MONTH(`date`)=07
    ORDER BY `date` ASC;
```

### Qual è il numero totale degli studenti iscritti? (5000)
```sql
    SELECT COUNT(*) AS `numero_studenti_iscritti_tot`
    FROM `students`;
```
---

# Query con GROUP BY

### Contare i corsi raggruppati per cfu
```sql
    SELECT COUNT(*) AS `corsi`, `cfu` 
    FROM `courses`
    GROUP BY `cfu`
    ORDER BY `cfu` ASC;
```

### Contare gli studenti raggruppati per anno di nascita
```sql
    SELECT COUNT(*) AS `studenti`, YEAR(`date_of_birth`) AS `anno_di_nascita`
    FROM `students`
    GROUP BY `anno_di_nascita`
    ORDER BY `anno_di_nascita` ASC;
```

### Selezionare il voto più basso dato ad ogni appello d'esame
```sql
    SELECT `exam_id` AS `esame`, MIN(`vote`) AS `voto_più_basso`
    FROM `exam_student`
    GROUP BY `esame`;
```

### Contare gli appelli d'esame del mese di luglio raggruppati per giorno
```sql
    SELECT COUNT(*) AS `appelli_esame_luglio`, DAY(`date`) as `giorno_esame`
    FROM `exams`
    WHERE MONTH(`date`)=07
    GROUP BY `giorno_esame`;
```