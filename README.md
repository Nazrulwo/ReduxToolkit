# ReduxToolkit
React, Redux Toolkit and TypeScript

STEP 1: Create React app with Redux toolkit, TypeScript and Vite
================================================================
npm create vite react-redux-ts-vite --template react-ts

Go to file: cd react-redux-ts-vite

STEP 2: Install Redux Toolkit and React-Redux:
==============================================
npm install @reduxjs/toolkit react-redux

STEP 3: Create a Redux slice for managing the state. In the src folder, create a file named counterSlice.ts:
============================================================================================================
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface CounterState {
  value: number;
}

const initialState: CounterState = {
  value: 0,
};

const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
  },
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;


STEP 4: Set up the Redux store. In the src folder, create a file named store.ts:
================================================================================

import { configureStore } from '@reduxjs/toolkit';

import counterReducer from './counterSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export type RootState = ReturnType<typeof store.getState>;

export type AppDispatch = typeof store.dispatch;

export default store;


STEP 5: Create a simple React component to interact with the Redux store. In the src folder, open App.tsx and replace its content with the following:
=====================================================================================================================================================

import React from 'react';

import { useSelector, useDispatch } from 'react-redux';

import { increment, decrement } from './counterSlice';

import { RootState, AppDispatch } from './store';

import './App.css';

function App() {
  const dispatch: AppDispatch = useDispatch();
  const count = useSelector((state: RootState) => state.counter.value);

  return (
    <div className="App">
      <header className="App-header">
        <p>Count: {count}</p>
        <div>
          <button onClick={() => dispatch(increment())}>Increment</button>
          <button onClick={() => dispatch(decrement())}>Decrement</button>
        </div>
      </header>
    </div>
  );
}

export default App;

STEP 6: Add index.tsx or main.tsx:
==================================

import { Provider } from 'react-redux';
import store from './app/store'; 
<Provider store={store}>
  <App /> 
</Provider>

STEP 7: Run the app:
==================
npm run dev

