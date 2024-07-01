<script setup>
import { reactive } from 'vue'

const state = reactive({
  inputValue: '',
  todoArray: []
})
const todoAdd = () => {
  if (state.inputValue == '') {
    alert('Please Add Your Task')
    return
  }
  const todoObj = {
    id: Date.now() + '',
    value: state.inputValue,
    fav: false,
    editable: false
  }
  console.log('click todoObj', todoObj)
  state.todoArray.push(todoObj)
  state.inputValue = ''
}
const deleteTodo = (todo) => {
  console.log(todo.id)
  // with refactoring
  state.todoArray = state.todoArray.filter((td) => td.id != todo.id)
  // without refactoring
  // const filterTodo =state.todoArray.filter(td => td.id != todo.id)
  // state.todoArray= filterTodo;
}
const editMe = (todo) => {
  console.log('editme', todo)
  todo.editable = true
}
const favMe = (todo) => {
  console.log(todo)
  todo.fav = true
}
</script>

<template>
  <main class="bg-gradient-to-r from-rose-600 to-indigo-600 h-screen">
    <nav class="bg-blue-600 flex justify-center p-4">
      <h1 class="text-white text-2xl">Your Todo App</h1>
    </nav>
    <div class="w-2/3 h-3/4 border-gray-900 rounded-xl mx-auto mt-4 p-4 bg-slate-200 shadow-xl">
      <div></div>
      <div class="flex">
        <input
          @keydown.enter="todoAdd"
          v-model="state.inputValue"
          class="text-xl p-2 w-11/12 rounded-2xl shadow-lg"
          placeholder="Your Todo"
          type="text"
        />
        <button class="bg-purple-900 text-white p-2 font-bold ml-2 rounded-lg" @click="todoAdd">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            version="1.1"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            width="40"
            height="36"
            x="0"
            y="0"
            viewBox="0 0 512 512"
            style="enable-background: new 0 0 512 512"
            xml:space="preserve"
            class=""
          >
            <g>
              <path
                fill="#581c87"
                fill-rule="evenodd"
                d="M256 0C114.8 0 0 114.8 0 256s114.8 256 256 256 256-114.8 256-256S397.2 0 256 0z"
                clip-rule="evenodd"
                opacity="1"
                data-original="#4bae4f"
                class=""
              ></path>
              <path
                fill="#ffffff"
                d="M116 279.6v-47.3c0-4.8 3.9-8.8 8.8-8.8h98.9v-98.8c0-4.8 3.9-8.8 8.8-8.8h47.3c4.8 0 8.7 3.9 8.7 8.8v98.9h98.8c4.8 0 8.8 3.9 8.8 8.8v47.3c0 4.8-3.9 8.7-8.8 8.7h-98.9v98.8c0 4.8-3.9 8.8-8.7 8.8h-47.3c-4.8 0-8.8-3.9-8.8-8.8v-98.9h-98.8c-4.9.1-8.8-3.9-8.8-8.7z"
                opacity="1"
                data-original="#ffffff"
                class=""
              ></path>
            </g>
          </svg>
        </button>
      </div>
      <div class="h-5/6 overflow-y-auto">
        <div
          v-for="todo in state.todoArray"
          :key="todo"
          class="flex gap-2 mt-2 bg-slate-50 justify-between p-2 rounded-lg"
        >
          <input
            v-if="todo.editable"
            @keydown.enter="todo.editable = false"
            v-model="todo.value"
            class="text-xl p-2 rounded-2xl"
            type="text"
          />
          <p v-else class="text-lg">
            {{ todo.value }}
          </p>
          <div class="flex gap-2">
            <button
              @click="deleteTodo(todo)"
              class="bg-red-500 text-white px-2 rounded-lg text-lg font-semibold shadow-lg"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                version="1.1"
                xmlns:xlink="http://www.w3.org/1999/xlink"
                width="30"
                height="30"
                x="0"
                y="0"
                viewBox="0 0 512 512"
                style="enable-background: new 0 0 512 512"
                xml:space="preserve"
                class=""
              >
                <g>
                  <path
                    fill="#ffffff"
                    fill-rule="evenodd"
                    d="M170.8 14.221A14.21 14.21 0 0 1 185 .014L326.991.006a14.233 14.233 0 0 1 14.2 14.223v35.117H170.8zm233.461 477.443a21.75 21.75 0 0 1-21.856 20.33H127.954a21.968 21.968 0 0 1-21.854-20.416L84.326 173.06H427.5l-23.234 318.6zm56.568-347.452H51.171v-33A33.035 33.035 0 0 1 84.176 78.2l343.644-.011a33.051 33.051 0 0 1 33 33.02v33zm-270.79 291.851a14.422 14.422 0 1 0 28.844 0V233.816a14.42 14.42 0 0 0-28.839-.01v202.257zm102.9 0a14.424 14.424 0 1 0 28.848 0V233.816a14.422 14.422 0 0 0-28.843-.01z"
                    opacity="1"
                    data-original="#fc0005"
                    class=""
                  ></path>
                </g>
              </svg>
            </button>

            <button
              class="bg-emerald-500 text-white px-2 rounded-lg text-lg font-semibold shadow-lg"
              @click="editMe(todo)"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                version="1.1"
                xmlns:xlink="http://www.w3.org/1999/xlink"
                width="24"
                height="24"
                x="0"
                y="0"
                viewBox="0 0 682.667 682.667"
                style="enable-background: new 0 0 512 512"
                xml:space="preserve"
              >
                <g>
                  <defs>
                    <clipPath id="a" clipPathUnits="userSpaceOnUse">
                      <path
                        d="M0 512h512V0H0Z"
                        fill="#000000"
                        opacity="1"
                        data-original="#000000"
                      ></path>
                    </clipPath>
                  </defs>
                  <g clip-path="url(#a)" transform="matrix(1.33333 0 0 -1.33333 0 682.667)">
                    <path
                      d="M0 0h-220c-22.092 0-40-17.908-40-40v-320c0-22.092 17.908-40 40-40h320c22.092 0 40 17.908 40 40v220"
                      style="
                        stroke-width: 30;
                        stroke-linecap: round;
                        stroke-linejoin: round;
                        stroke-miterlimit: 10;
                        stroke-dasharray: none;
                        stroke-opacity: 1;
                      "
                      transform="translate(275 415)"
                      fill="none"
                      stroke="#ffffff"
                      stroke-width="30"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-miterlimit="10"
                      stroke-dasharray="none"
                      stroke-opacity=""
                      data-original="#000000"
                      opacity="1"
                    ></path>
                    <path
                      d="m0 0-226.274-226.273-70.711-14.143 14.142 70.711L-56.569 56.569c7.81 7.81 20.474 7.81 28.284 0L0 28.284C7.81 20.474 7.81 7.811 0 0Z"
                      style="
                        stroke-width: 30;
                        stroke-linecap: round;
                        stroke-linejoin: round;
                        stroke-miterlimit: 10;
                        stroke-dasharray: none;
                        stroke-opacity: 1;
                      "
                      transform="translate(491.143 434.573)"
                      fill="none"
                      stroke="#ffffff"
                      stroke-width="30"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-miterlimit="10"
                      stroke-dasharray="none"
                      stroke-opacity=""
                      data-original="#000000"
                      opacity="1"
                    ></path>
                    <path
                      d="m0 0 56.568-56.568"
                      style="
                        stroke-width: 30;
                        stroke-linecap: round;
                        stroke-linejoin: round;
                        stroke-miterlimit: 10;
                        stroke-dasharray: none;
                        stroke-opacity: 1;
                      "
                      transform="translate(406.29 462.857)"
                      fill="none"
                      stroke="#ffffff"
                      stroke-width="30"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-miterlimit="10"
                      stroke-dasharray="none"
                      stroke-opacity=""
                      data-original="#000000"
                      opacity="1"
                    ></path>
                  </g>
                </g>
              </svg>
            </button>

            <button
              class="bg-pink-500 text-white px-2 rounded-lg text-lg font-semibold shadow-lg"
              @click="favMe(todo)"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                version="1.1"
                xmlns:xlink="http://www.w3.org/1999/xlink"
                width="36"
                height="36"
                x="0"
                y="0"
                viewBox="0 0 511.855 511.855"
                style="enable-background: new 0 0 512 512"
                xml:space="preserve"
              >
                <g>
                  <path
                    d="M466.186 74.688C436.688 45.19 397.47 28.945 355.754 28.945c-36.894 0-71.836 12.708-99.827 36.051-27.989-23.343-62.933-36.051-99.825-36.051-41.716 0-80.936 16.245-110.433 45.743-60.891 60.891-60.892 159.97 0 220.865l171.249 171.249c10.389 10.387 24.242 16.107 39.01 16.107s28.621-5.721 39.01-16.108l171.248-171.248c60.892-60.894 60.892-159.974 0-220.865z"
                    :fill="todo.fav ? '#000000' : '#ffffff'"
                    opacity="1"
                    data-original="#000000"
                  ></path>
                </g>
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
