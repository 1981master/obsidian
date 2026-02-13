```typescript
/******************************************************************
REACT EVENTS + React.FC EXPLAINED
******************************************************************/

import React, { useState } from "react";


/* ================================================================
1️⃣ WHAT IS React.FC ?
================================================================ */

/*
React.FC = React.FunctionComponent

It is a generic type for typing functional components.

Example:
React.FC<PropsType>

It automatically:
✔ Types props
✔ Adds children?: ReactNode automatically
*/

type CardProps = {
    title: string;
};

const Card: React.FC<CardProps> = ({ title, children }) => {
    return (
        <div>
            <h3>{title}</h3>
            {children}
        </div>
    );
};

/*
WITHOUT React.FC (modern preferred way)
*/

const CardBetter = ({ title }: CardProps) => {
    return <h3>{title}</h3>;
};

/*
🔥 Modern best practice:
Avoid React.FC unless you need automatic children typing.
Just type props directly.
*/


/* ================================================================
2️⃣ COMMON REACT EVENT TYPES
================================================================ */

const EventExamples = () => {

    const [value, setValue] = useState<string>("");

    /* ------------------------------------------------------------
    INPUT CHANGE
    ------------------------------------------------------------ */

    const handleInputChange = (
        e: React.ChangeEvent<HTMLInputElement>
    ): void => {
        setValue(e.target.value);
    };

    /* ------------------------------------------------------------
    TEXTAREA CHANGE
    ------------------------------------------------------------ */

    const handleTextareaChange = (
        e: React.ChangeEvent<HTMLTextAreaElement>
    ): void => {
        console.log(e.target.value);
    };

    /* ------------------------------------------------------------
    SELECT CHANGE
    ------------------------------------------------------------ */

    const handleSelectChange = (
        e: React.ChangeEvent<HTMLSelectElement>
    ): void => {
        console.log(e.target.value);
    };

    /* ------------------------------------------------------------
    FORM SUBMIT
    ------------------------------------------------------------ */

    const handleSubmit = (
        e: React.FormEvent<HTMLFormElement>
    ): void => {
        e.preventDefault();
        console.log("Form submitted");
    };

    /* ------------------------------------------------------------
    BUTTON CLICK
    ------------------------------------------------------------ */

    const handleClick = (
        e: React.MouseEvent<HTMLButtonElement>
    ): void => {
        console.log("Button clicked");
    };

    /* ------------------------------------------------------------
    DIV CLICK
    ------------------------------------------------------------ */

    const handleDivClick = (
        e: React.MouseEvent<HTMLDivElement>
    ): void => {
        console.log("Div clicked");
    };

    /* ------------------------------------------------------------
    KEYBOARD EVENT
    ------------------------------------------------------------ */

    const handleKeyDown = (
        e: React.KeyboardEvent<HTMLInputElement>
    ): void => {
        if (e.key === "Enter") {
            console.log("Enter pressed");
        }
    };

    /* ------------------------------------------------------------
    FOCUS EVENT
    ------------------------------------------------------------ */

    const handleFocus = (
        e: React.FocusEvent<HTMLInputElement>
    ): void => {
        console.log("Input focused");
    };

    /* ------------------------------------------------------------
    BLUR EVENT
    ------------------------------------------------------------ */

    const handleBlur = (
        e: React.FocusEvent<HTMLInputElement>
    ): void => {
        console.log("Input lost focus");
    };

    /* ------------------------------------------------------------
    UI
    ------------------------------------------------------------ */

    return (
        <div onClick={handleDivClick}>

            <form onSubmit={handleSubmit}>
                <input
                    type="text"
                    value={value}
                    onChange={handleInputChange}
                    onKeyDown={handleKeyDown}
                    onFocus={handleFocus}
                    onBlur={handleBlur}
                />

                <textarea onChange={handleTextareaChange} />

                <select onChange={handleSelectChange}>
                    <option value="1">One</option>
                    <option value="2">Two</option>
                </select>

                <button type="submit" onClick={handleClick}>
                    Submit
                </button>
            </form>

        </div>
    );
};

export default EventExamples;


/******************************************************************
CHEAT SHEET — EVENT TYPES

React.ChangeEvent<HTMLInputElement>
React.ChangeEvent<HTMLTextAreaElement>
React.ChangeEvent<HTMLSelectElement>

React.FormEvent<HTMLFormElement>

React.MouseEvent<HTMLButtonElement>
React.MouseEvent<HTMLDivElement>

React.KeyboardEvent<HTMLInputElement>

React.FocusEvent<HTMLInputElement>


******************************************************************/

/******************************************************************
React.FC SUMMARY

React.FC<Props> = React.FunctionComponent<Props>

Pros:
✔ Includes children automatically
✔ Explicit return type ReactElement

Cons:
❌ Children always allowed (even if you don’t want them)
❌ Slightly more verbose
❌ Modern React team discourages overuse

🔥 Recommended in 2026:
Use plain function component with typed props:

const MyComponent = ({ title }: Props) => { }

******************************************************************/

```