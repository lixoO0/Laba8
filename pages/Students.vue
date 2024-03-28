<template>
  <div>
    <h1>Список студентів</h1>

    <div>
      <!-- Пошук -->
      <input type="text" v-model="searchQuery" placeholder="Пошук студента" style="margin-bottom: 10px; color: white;">

      <!-- Таблиця зі списком студентів -->
      <table>
        <thead>
        <tr>
          <th>Ім'я</th>
          <th>Прізвище</th>
          <th>Група</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="student in paginatedStudents" :key="student.id">
          <td>{{ student.firstName }}</td>
          <td>{{ student.lastName }}</td>
          <td>{{ student.group }}</td>
        </tr>
        </tbody>
      </table>
    </div>

    <!-- Пагінація -->
    <button @click="previousPage" :disabled="currentPage === 1">Попередня сторінка</button>
    <span>Сторінка {{ currentPage }} з {{ totalPages }}</span>
    <button @click="nextPage" :disabled="currentPage === totalPages">Наступна сторінка</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      students: [], // Список студентів
      searchQuery: '', // Пошуковий запит
      currentPage: 1, // Поточна сторінка
      itemsPerPage: 5 // Кількість елементів на сторінці
    };
  },
  computed: {
    // Обчислення загальної кількості сторінок
    totalPages() {
      return Math.ceil(this.filteredStudents.length / this.itemsPerPage);
    },
    // Фільтрація студентів за пошуковим запитом
    filteredStudents() {
      return this.students.filter(student =>
        student.firstName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        student.lastName.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
        student.group.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    // Відфільтрований список студентів для поточної сторінки
    paginatedStudents() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.filteredStudents.slice(startIndex, endIndex);
    }
  },
  methods: {
    // Перехід на попередню сторінку
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    // Перехід на наступну сторінку
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    }
  },
  mounted() {
    // Метод для отримання списку студентів (може бути AJAX-запит)
    // Приклад:
    this.students = [
      { id: 1, firstName: 'Іван', lastName: 'Петров', group: 'Група 1' },
      { id: 2, firstName: 'Марія', lastName: 'Іванова', group: 'Група 2' },
      { "id": 3, "firstName": "Олександр", "lastName": "Сидоренко", "group": "Група 3" },
      { "id": 4, "firstName": "Анна", "lastName": "Павлюченко", "group": "Група 4" },
      { "id": 5, "firstName": "Сергій", "lastName": "Ковальчук", "group": "Група 5" },
      { "id": 6, "firstName": "Ольга", "lastName": "Михайленко", "group": "Група 6" },
      { "id": 7, "firstName": "Віталій", "lastName": "Лисенко", "group": "Група 7" },
      { "id": 8, "firstName": "Тетяна", "lastName": "Захарченко", "group": "Група 8" },
      { "id": 9, "firstName": "Євген", "lastName": "Григоренко", "group": "Група 9" },
      { "id": 10, "firstName": "Ірина", "lastName": "Кузьменко", "group": "Група 10" },
      { "id": 11, "firstName": "Андрій", "lastName": "Бондаренко", "group": "Група 11" },
      { "id": 12, "firstName": "Наталія", "lastName": "Поліщук", "group": "Група 12" },
      { "id": 13, "firstName": "Максим", "lastName": "Горбачов", "group": "Група 13"},
      {"id": 14, "firstName": "Олена", "lastName": "Мельник", "group": "Група 14"},
      {"id": 15, "firstName": "Віктор", "lastName": "Левченко", "group": "Група 15"},
      {"id": 16, "firstName": "Марина", "lastName": "Шевченко", "group": "Група 16"},
      {"id": 17, "firstName": "Ігор", "lastName": "Іванченко", "group": "Група 17"},
      {"id": 18, "firstName": "Оксана", "lastName": "Ковальова", "group": "Група 18"},
      {"id": 19, "firstName": "Денис", "lastName": "Кравченко", "group": "Група 19"},
      {"id": 20, "firstName": "Софія", "lastName": "Федоренко", "group": "Група 20"},
      {"id": 21, "firstName": "Роман", "lastName": "Григорович", "group": "Група 21"}

      // Додайте інші дані за потреби
    ];
  }
};
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  color: black;
  background-color: #f2f2f2;
}

/* Зміна кольору рядків при наведенні миші */
tr:hover {
  color: black;
  background-color: #f5f5f5;
}

</style>
