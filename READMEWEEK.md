# assignment 12 react hooks practice

## STEP 2. Source Code Exploration
Project Structure: App.jsx는 네 개의 lsb을 탭으로 보여주는 화면을 구성한다. lab1은 useEffect를 사용해서 타이머를 구현하고, lab2는 start나 stop의 상태에 따라 타이머를 조정하고, lab3는 useRef를 이용해 focus와 clear 버튼이 작동하도록 하고, lab4는 useRef로 타이머를 구현한다. 

useEffect: useEffect에서는 dependency array에 무엇을 넣느냐에 따라 실행시점이 달라지고, effect가 clearup을 반환한디. effect가 다시 실행되기 전에 호출되어 타이머를 정리한다.

useRef: useRef는 current 객체를 반환히고 current가 바뀌어도 렌더링하지 않는다. useState에서는 값 변경되면 화면을 다시 렌더링한다. 

Code Analysis: 
lab2: 
useEffect(() => {
  if (!running) return;

  const timerId = setInterval(() => {
    setCount(prev => prev + 1);
  }, 1000);

  return () => clearInterval(timerId);
}, [running]);
running이 true가 되면 1초마다 count를 증가시키는 타이머를 작동시키고 running이 바뀌거나 컴포넌트가 사라질 때 cleanup함수가 실행되어 타이머를 정리해 중복 실행을 방지한다. running아 false면 타이머를 종료한다. 

lab3:
const inputRef = useRef(null);

const focusInput = () => {
  inputRef.current?.focus();
};

return (
  <input
    id="student-name"
    ref={inputRef}
    placeholder="Enter your name"
  />
);
useRef(null)은 ref 객체를 만들고, <input ref={inputRef}>로 연결하여 렌더링하면 inputRef.current가 입력창으로 커서를 옮겨 타이핑할 수 있게 한다. 

## STEP3. Lab 비교 분석
useEffect의 Dependency Array가 필요한 이유는?: effect를 언제 다시 실행할지 정해야 하기 때문에 필요하다. lab2에서는 [running]을 사용해 실행 상태가 바뀔때만 타이머를 다시 설정한다. 

Cleanup을 사용하지 않으면 어떤 문제가 발생할 수 있는가?: 타이머가 계속 남아서 중복으로 실행되거나 컴포넌트가 사라진 뒤에도 작동하고 있을 수 있는 문제가 발생한다. 

useState와 useRef의 가장 중요한 차이는?: useState를 바꾸면 화면이 다시 렌더링되지만 useRef는 .current가 바뀌어도 다시 렌더링 되지 않는다. 

LAB 2와 LAB 4의 Timer 관리 방식은 어떻게 다른가?: lab2는 running 상태에 따라 useEffect가 타이머를 시작하고 cleanup으로 정리한다. 반면 lab4는 버튼 함수에서 useRef에 저장한 타이머를 직접 시작/중지하고 언마운트 시 cleanup으로 interval을 정리한다. 

## STEP 4. Customizing
프로젝트 제목 또는 설명 변경: App.jsx / 프로젝트 제목과 설명 변경
CSS 스타일 2곳 이상 변경: App.css / 배경 색 변경, 글자색 변경
4개 Lab 정상 동작 확인: lab 1~4 todo 수정

선택 기능 (추가 평가)
Timer 실행 상태 표시: lab2, 4 / timer 실행 상태를 표시하도록 수정

## weekly review
새롭게 배운 내용 3가지: useEffect를 활용한 timer 구현과 cleanup방법, UseRef를 활용한 timer 구현, 그리고 useEffect와 useRef의 차이를 배웠다.

어려웠던 점과 해결 방법: timer 실행 상태를 표시하는 부분에서 어려움을 느꼈다. ai를 통해서 어떻게 수정해야 하고 수정된 코드가 어떤 의미를 가지고 있는지 배울 수 있었다. 

AI 활용 내용 및 느낀 점: timer 실행 상태를 표시하는 부분에서 ai를 활용했다. 프로젝트를 통해서 각 hook의 역할을 잘 이해할 수 있었다. 