# Вопросы на тему «CSS-in-JS»

## Вопросы простые

### 1 - Что есть результат выполнения функции `styled.tagname`?

```jsx
import styled from 'styled-components';

const StyledElement = styled.div`
  width: 100px;
  height: 100px;

  background-color: coral;
`;
```

Варианты ответа:
- [ ] Класс, который нужно добавить какому-либо элементу `<div>`
- [x] React-компонент

> Вопрос проверяет понимание работы функции `styled.tagname` (или `styled(Component)`)
>
> Функция создает react-компонент, который можно добавить в JSX

### 2 - Что есть результат выполнения функции `createGlobalStyle`?

```jsx
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
  font-family: Arial, sans-serif;
  color: black;
`;
```

Варианты ответа:
- [ ] Класс, который нужно добавить элементу `<body>`
- [x] React-компонент
- [ ] Функция `createGlobalStyle` подключает глобальные стили к документу и ничего не возвращает

> Вопрос проверяет понимание работы функции `createGlobalStyle`
>
> Функция создает react-компонент, который можно добавить в JSX

### 3 - Меняется ли цвет отображаемого элемента при наведении?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled from 'styled-components';

const StyledElement = styled.div({
  width: 100,
  height: 100,

  backgroundColor: 'coral',

  hover: {
    backgroundColor: 'tomato'
  }
});

const App = () => <StyledElement />;

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Код работает корректно - цвет элемента меняется при наведении
- [x] Чтобы цвет элемента менялся при наведении, нужно поправить название поля `hover` на `':hover'`
- [ ] Синтаксис объектов не поддерживает псевдоклассы, поэтому нужно реализовать элемент в синтаксисе шаблонных строк

> Вопрос проверяет знание синтаксиса объектов
>
> Синтаксис объектов поддерживает псевдоклассы, но для корректной работы кода нужно поправить название поля

## Вопросы средние

### 4 - Что есть результат выполнения функции `keyframes`?

```jsx
import styled, { keyframes } from 'styled-components';

const rotation = keyframes`
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
`;

const StyledElement = styled.div`
  animation: ${rotation} 1s infinite;
`;
```

Варианты ответа:
- [ ] Название анимации
- [ ] React-компонент
- [x] Объект с описанием анимации

> Вопрос проверяет понимание работы функции `keyframes`
>
> Функция создает объект-модель анимации, и `styled-components` использует этот объект при подключении анимации к элементам

### 5 - Какого цвета кнопка?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled from 'styled-components';

const Button = ({ children }) => <button>{children}</button>;

const StyledButton = styled(Button)`
  background-color: coral;
`;

const App = () => <StyledButton>Кнопка</StyledButton>;

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] В библиотеке `styled-components` все предусмотрено - стили автоматически применяются к корневому элементу react-компонента, поэтому кнопка коралловая
- [x] Чтобы кнопка окрасилась в коралловый цвет, компонент `Button` должен пробрасывать проп `className`
- [ ] Чтобы кнопка окрасилась в коралловый цвет, компонент `Button` должен пробрасывать реф

> Вопрос проверяет понимание механизма создания react-компонентов, совместимых с функцией `styled(Component)`
>
> Чтобы react-компонент можно было как-либо кастомизировать при помощи фабрики `styled`, этот компонент должен пробрасывать проп `className`

### 6 - Какого цвета кнопка?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled, { ThemeProvider } from 'styled-components';

const StyledButton = styled.button`
  background-color: ${(props) => props.theme.buttonColor};
`;

const App = () => (
  <ThemeProvider theme={{ buttonColor: 'coral' }}>
    <ThemeProvider theme={{ buttonColor: 'tomato' }} />
    <StyledButton>Кнопка</StyledButton>
  </ThemeProvider>
);

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Кнопка никак не окрашена, потому что вложенные провайдеры конфликтуют
- [x] Кнопка кораллового цвета
- [ ] Кнопка томатного цвета

> Вопрос проверяет понимание работы провайдеров в react в целом и провайдеров темы в частности
>
> Кнопка вложена только в первый внешний провайдер, поэтому принимает цвет от него

### 7 - Какого цвета отображаемый элемент?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled, { createGlobalStyle } from 'styled-components';

createGlobalStyle`
  div {
    background-color: coral !important;
  }
`;

const StyledElement = styled.div`
  width: 100px;
  height: 100px;

  background-color: tomato;
`;

const App = () => <StyledElement />;

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Отображаемый элемент кораллового цвета
- [x] Отображаемый элемент томатного цвета

> Для ответа на этот вопрос нужно понимать, что функция `createGlobalStyle` создает react-компонент, который при рендере добавляет глобальные стили
>
> В кейсе созданный react-компонент никуда не рендерится (результат выполнения функции `createGlobalStyle` даже не сохраняется в переменную), поэтому глобальные стили с `!important` не попадают в документ

### 8 - Какие атрибуты получает DOM-элемент кнопки?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled, { css } from 'styled-components';

const StyledButton = styled.button`
  ${(props) => props.block && css`
    display: block;
    width: 100%;
  `}

  cursor: ${(props) => props.disabled ? 'not-allowed' : 'pointer'};
`;

const App = () => (
  <StyledButton block disabled>
    Кнопка
  </StyledButton>
);

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Элемент вообще не получает атрибуты
- [ ] Элемент получает атрибут `class`
- [x] Элемент получает атрибуты `class` и `disabled`
- [ ] Элемент получает атрибуты `class`, `block` и `disabled`

> Вопрос проверяет понимание того, как `styled-components` работает с пропами в случае стилизуемых стандартных html-тегов
>
> Соответствующие DOM-элементы получают только стандартные атрибуты

### 9 - Какие пропы получает компонент `Button`?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled, { css } from 'styled-components';

const Button = ({ children, ...rest }) => (
  <button {...rest}>
    { children }
  </button>
);

const StyledButton = styled(Button)`
  ${(props) => props.block && css`
    display: block;
    width: 100%;
  `}

  cursor: ${(props) => props.disabled ? 'not-allowed' : 'pointer'};
`;

const App = () => (
  <StyledButton block disabled>
    Кнопка
  </StyledButton>
);

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Компонент получает проп `children`
- [ ] Компонент получает пропы `className` и `children`
- [ ] Компонент получает пропы `className`, `disabled` и `children`
- [x] Компонент получает пропы `className`, `block`, `disabled` и `children`

> Вопрос проверяет понимание того, как `styled-components` работает с пропами в случае стилизуемых react-компонентов
>
> Стилизуемые react-компоненты получают все пропы без исключений

## Вопросы сложные

### 10 - Каким образом стили отображаемого элемента подключаются к документу?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled from 'styled-components';

const StyledElement = styled.div`
  width: 100px;
  height: 100px;

  background-color: coral;
`;

const App = () => <StyledElement />;

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Стили подключаются при помощи отдельного файла. В стилях указано правило с селектором по тегу `<div>`
- [ ] Стили подключаются при помощи отдельного файла. В стилях указано правило с селектором по уникальному классу
- [ ] Стили указываются внутри элемента `<style>`, который в свою очередь расположен внутри элемента `<head>`. В стилях указано правило с селектором по тегу `<div>`
- [x] Стили указываются внутри элемента `<style>`, который в свою очередь расположен внутри элемента `<head>`. В стилях указано правило с селектором по уникальному классу
- [ ] Стили указываются в атрибуте `style` отображаемого элемента

> Вопрос проверяет понимание основного механизма CSS-in-JS - как описанные стили попадают в документ и применяются к элементам?

### 11 - Какие стили подключаются к документу?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled from 'styled-components';

const StyledElementFirst = styled.div`
  width: 100px;
  height: 100px;

  background-color: coral;
`;

const StyledElementSecond = styled.div`
  width: 200px;
  height: 200px;

  background-color: tomato;
`;

const StyledElementThird = styled.div`
  width: 300px;
  height: 300px;

  background-color: aquamarine;
`;

const App = () => {
  const potentiallyUsedElement = <StyledElementFirst />;

  return <StyledElementSecond />;
};

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [x] Подключаются стили только для второго элемента
- [ ] Подключаются стили для первого и второго элементов
- [ ] Подключаются стили для всех элементов

> Вопрос проверяет понимание того, как `styled-components` выделяет необходимые стили - в любой момент к документу подключены стили только тех элементов, которые расположены в DOM

### 12 - Какого цвета отображаемый элемент?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled from 'styled-components';

const StyledParent = styled.div`
  width: 100px;
  height: 100px;

  background-color: coral !important;
`;

const StyledChildren = styled(StyledParent)`
  background-color: tomato;
`;

const App = () => <StyledChildren />;

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [x] Отображаемый элемент кораллового цвета
- [ ] Отображаемый элемент томатного цвета

> Вопрос проверяет понимание механизма расширения одного стайлед-компонента другим
>
> Свойства "ребенка" не перезаписывают свойства "родителя", а объединяются с ними - итоговое правило для элемента `StyledChildren` выглядит так:
> ```css
> .uniqueClass {
>   width: 100px;
>   height: 100px;
>
>   background-color: coral !important;
>   background-color: tomato;
> }
> ```

### 13 - Какой элемент попадает в DOM?

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import styled from 'styled-components';

const StyledElement = styled.button.attrs({ type: "button" })`
  border: 1px solid coral;
`;

const App = () => <StyledElement as="input" type="text" />;

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Варианты ответа:
- [ ] Элемент `button` с атрибутом `type="button"`
- [ ] Элемент `button` с атрибутом `type="text"`
- [x] Элемент `input` с атрибутом `type="button"`
- [ ] Элемент `input` с атрибутом `type="text"`

> Вопрос проверяет понимание работы метода `attrs` и пропа `as`
>
> Если в метод `attrs` передать статичный объект, переопределить значения соответствующих атрибутов не получится
