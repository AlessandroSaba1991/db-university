# QUERY GROUP BY:

## Contare quanti iscritti ci sono stati ogni anno
- SELECT COUNT(`id`) AS `num_students`, year(`enrolment_date`) AS `year_enrolment` 
  FROM `students` 
  GROUP BY year(`enrolment_date`);

## Contare gli insegnanti che hanno l'ufficio nello stesso edificio
- SELECT COUNT(`id`) AS `Num_teachers`, `office_address`
  FROM `teachers`
  GROUP BY  `office_address`;

## Calcolare la media dei voti di ogni appello d'esame
- SELECT `exam_id` ,avg(`vote`) AS `avg_vote`
  FROM `exam_student`
  GROUP BY `exam_id`;

## Contare quanti corsi di laurea ci sono per ogni dipartimento
- SELECT `department_id`, COUNT(`id`) AS `num_degrees`
  FROM `degrees`
  GROUP BY `department_id`;

_______________________________________________________________________

# QUERY JOINS:

## Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
- SELECT `students`. `name`, `students`. `surname`,`degrees`. `name` AS `degree_name`
  FROM `degrees`
  JOIN `students` ON `students`. `degree_id` = `degrees`.`id`
  WHERE `degrees`.`name` = "Corso di Laurea in Economia"  
  ORDER BY `students`.`name`;

## Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
- SELECT `departments`.`name` AS `departments_name`, `degrees`.`name` AS `degree_name`, `degrees`.`level`
  FROM `departments`
  JOIN `degrees` ON `degrees`.`department_id` = `departments`.`id`
  WHERE `departments`.`name` = "Dipartimento di Neuroscienze"
  AND `degrees`.`level` = "magistrale";

## Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
- SELECT  `teachers`.`id` AS `teacher_id`,`teachers`.`name`, `teachers`.`surname`,`courses`.`name` AS `course_name`
  FROM `teachers` 
  JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
  JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
  WHERE `teachers`.`name` = "Fulvio"
  AND `teachers`.`surname` = "Amato";  

## Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
- SELECT `students`. `surname`,`students`. `name`, `departments`.`name` AS `department_name`, `degrees`.`name` AS `degree_name`,`degrees`.`level` AS `degree_level`,`degrees`.`address` AS `degree_address`,`degrees`.`email` AS `degree_email`,`degrees`.`website` AS `degree_website`
  FROM `students`
  JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
  JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
  ORDER BY `students`.`surname`, `students`.`name`;

## Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
- SELECT `degrees`. `name` AS  `degree_name`,`courses`. `name` AS `course_name`, `teachers`.`name` AS `teacher_name`,`teachers`.`surname` AS `teacher_surname`
  FROM `degrees`
  JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
  JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
  JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
  ORDER BY `degree_name`;

## Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
- SELECT DISTINCT `departments`.`name` AS `department_name`, `teachers`.`surname` AS `teacher_surname`, `teachers`.`name` AS `teacher_name`
  FROM `departments`
  JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` 
  JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id` 
  JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
  JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
  WHERE `departments`.`name` = "Dipartimento di Matematica"
  ORDER BY `teachers`.`surname`, `teachers`.`name`;

## BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami
- SELECT `students`. `surname` AS `student_surname`,`students`. `name` AS `student_name`,`courses`. `name`, COUNT(`exam_student`.`vote`) AS `attemps`
  FROM `exam_student`
  JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
  JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
  JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
  WHERE `exam_student`.`vote`<18
  GROUP BY `courses`.`id`, `students`. `id`
  ORDER BY `students`. `surname`, `students`. `name`;