# Вопросы на тему «CSS-in-JS»

## Вопросы простые

### Меняется ли цвет отображаемого элемента при наведении?

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

### Какого цвета кнопка?

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

### Какого цвета отображаемый элемент?

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

## Вопросы средние

### Какого цвета кнопка?

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

### Каким образом стили отображаемого элемента подключаются к документу?

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
- [ ] Стили подключаются при помощи отдельного файла
- [ ] Стили указываются в атрибуте `style` отображаемого элемента
- [x] Стили указываются внутри элемента `<style>`, который в свою очередь расположен внутри элемента `<head>`

## Вопросы сложные

### Какого цвета отображаемый элемент?

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

### Какие стили подключаются к документу?

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
