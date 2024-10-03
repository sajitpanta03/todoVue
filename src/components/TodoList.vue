<script setup lang="ts">
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from "@/components/ui/select";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import { Button } from "@/components/ui/button";
import { onMounted, ref, watch } from "vue";
import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
} from "@/components/ui/table";

interface Task {
  id: string;
  name: string;
  level: string;
  completed: boolean;
}

const levels: string[] = [
  "Beginner Level",
  "Advance Beginner Level",
  "Mid Level",
  "Full Stack Mid Level",
  "Senior Level",
];

const selectedLevel = ref<string>("");
const taskName = ref<string>("");
const completed = ref<boolean>(false);
const todos = ref<Task[]>([]); 
const editingTaskId = ref<string | null>(null);

function generateId(): string {
  return Date.now().toString() + Math.random().toString(16).substr(2);
}

function addOrUpdateTask(): void {
  if (editingTaskId.value) {
    const taskIndex = todos.value.findIndex(
      (task) => task.id === editingTaskId.value
    );
    if (taskIndex !== -1) {
      todos.value[taskIndex].name = taskName.value;
      todos.value[taskIndex].level = selectedLevel.value;
      todos.value[taskIndex].completed = completed.value; 
    }
    editingTaskId.value = null; 
  } else {
    const task: Task = {
      id: generateId(),
      name: taskName.value,
      level: selectedLevel.value,
      completed: completed.value, 
    };
    todos.value.push(task);
  }
  localStorage.setItem("todos", JSON.stringify(todos.value));
  taskName.value = "";
  selectedLevel.value = ""; 
  completed.value = false; 
}

function updateTaskCompletion(task: Task): void {
  localStorage.setItem("todos", JSON.stringify(todos.value));
}

function removeTaskById(id: string): void {
  todos.value = todos.value.filter((task) => task.id !== id);
  localStorage.setItem("todos", JSON.stringify(todos.value));
}

function editTaskById(id: string): void {
  const taskToEdit = todos.value.find((task) => task.id === id);
  if (taskToEdit) {
    taskName.value = taskToEdit.name;
    selectedLevel.value = taskToEdit.level;
    completed.value = taskToEdit.completed;
    editingTaskId.value = id;
  }
}

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
);

onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem("todos") || "[]");
});

const groupedTasks = ref<Record<string, Task[]>>({});
watch(
  todos,
  (newTasks) => {
    groupedTasks.value = newTasks.reduce(
      (acc: Record<string, Task[]>, task: Task) => {
        if (!acc[task.level]) {
          acc[task.level] = [];
        }
        acc[task.level].push(task);
        return acc;
      },
      {}
    );
  },
  { deep: true }
);
</script>

<template>
  <div class="flex items-center justify-center mt-10">
    <Card class="w-[350px]">
      <CardHeader>
        <CardTitle>{{ editingTaskId ? "Edit Task" : "Create Task" }}</CardTitle>
        <CardDescription>Task your new project in one-click.</CardDescription>
      </CardHeader>
      <CardContent>
        <form @submit.prevent="addOrUpdateTask">
          <div class="grid items-center w-full gap-4">
            <div class="flex flex-col space-y-1.5">
              <Label for="name">Name</Label>
              <Input
                id="name"
                v-model="taskName"
                placeholder="Name of your project"
              />
            </div>
            <div class="flex flex-col space-y-1.5">
              <Label for="framework">Level</Label>
              <Select v-model="selectedLevel">
                <SelectTrigger id="framework">
                  <SelectValue placeholder="Select" />
                </SelectTrigger>
                <SelectContent position="popper">
                  <SelectItem
                    v-for="(level, index) in levels"
                    :key="index"
                    :value="level"
                  >
                    {{ level }}
                  </SelectItem>
                </SelectContent>
              </Select>
            </div>
            <div class="flex flex-col space-y-1.5">
              <Label for="completed">Completed</Label>
              <!-- Normal Checkbox -->
              <input
                type="checkbox"
                id="completed"
                v-model="completed"
                @change="updateTaskCompletion({ completed })"
              />
              <Label :for="completed">Completed</Label>
            </div>
          </div>
        </form>
      </CardContent>
      <CardFooter class="flex justify-between px-6 pb-6">
        <Button
          variant="outline"
          @click="
            taskName.value = '';
            selectedLevel.value = '';
            completed.value = false; // Reset completion status on cancel
            editingTaskId.value = null; // Reset editing state on cancel
          "
          >Cancel</Button
        >
        <Button @click="addOrUpdateTask">{{
          editingTaskId ? "Edit Task" : "Add Task"
        }}</Button>
      </CardFooter>
    </Card>
  </div>

  <div class="p-4 mt-10 md:px-60">
    <div class="border rounded-md">
      <div v-for="(tasks, level) in groupedTasks" :key="level">
        <h2 class="text-xl font-bold">{{ level }}</h2>
        <Table>
          <TableHeader>
            <TableRow>
              <TableHead>Task Name</TableHead>
              <TableHead>Completed</TableHead>
              <TableHead>Action</TableHead>
            </TableRow>
          </TableHeader>
          <TableBody>
            <TableRow v-for="(task, index) in tasks" :key="task.id">
              <TableCell>{{ task.name }}</TableCell>
              <TableCell>
                <!-- Normal Checkbox for task completion -->
                <input
                  type="checkbox"
                  v-model="task.completed"
                  @change="updateTaskCompletion(task)"
                />
              </TableCell>
              <div class="grid space-y-1">
                <Button
                  class="w-12 h-8 text-white bg-red-600 hover:bg-red-800 dark:text-black"
                  @click="removeTaskById(task.id)"
                  >Delete</Button
                >
                <Button
                  class="w-12 h-8 text-white bg-sky-700 hover:bg-sky-800 dark:text-black"
                  @click="editTaskById(task.id)"
                  >Edit</Button
                >
              </div>
            </TableRow>
            <TableRow v-if="tasks.length === 0">
              <TableCell class="h-24 text-center" colspan="3"
                >No tasks found.</TableCell
              >
            </TableRow>
          </TableBody>
        </Table>
      </div>
    </div>
  </div>
</template>
