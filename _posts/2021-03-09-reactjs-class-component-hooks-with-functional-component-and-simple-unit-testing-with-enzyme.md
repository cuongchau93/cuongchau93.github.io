---
title: ReactJS class component => hooks with functional component and simple unit
  testing with Enzyme
---

To start off, consider the following class component
```prettyprint
import React from 'react';
import ReactDOM from 'react-dom';
// some external css file, it should be added by import './styling.css';
// .toggleOn {
//     color: red;
//   }
// .toggleOff {
//     color: green;
//   }

// class component
class Toggle extends React.Component {
    constructor(props) { 
        super(props);
        this.state = {
            isOn: false
        };

        this.handleClick = this.handleClick.bind(this);
    }

    handleClick() {
        //async setState because 
        this.setState(state => ({
            isToggleOn: !state.isToggleOn
          }));
    }

  render() {
    return (
        <button onClick={this.handleClick} className={this.state.isOn ? "toggleOn" : "toggleOff"}> {this.state.isOn ? 'ON' : 'OFF'}</button>
    );
  }
}

ReactDOM.render(<Toggle />, document.getElementById('root'));
```

With latest version of ReactJS, we can use functional component with hook to make it cleaner

```prettyprint
import React from 'react';
import ReactDOM from 'react-dom';

// functional component with hooks
const Toggle = () => {
    const [isOn, setIsOn] = useState(false);

    const handleClick = () => {
        setIsOn(!isOn);
    }

    return (
        <button onClick={handleClick} className={isOn ? "toggleOn" : "toggleOff"}> {isOn ? 'ON' : 'OFF'}</button>
    )
}; 

ReactDOM.render(<Toggle />, document.getElementById('root'));
```

We can finish it off with simple unit testing with Enzyme

```prettyprint
// add in some unit tests with jest
import Enzyme, { shallow } from 'enzyme'

describe('Toggle Test', () => {
    it('given default state', () => {
        it('should be able to switch to ON if clicked', () => {
            const wrapper = shallow(<Toggle/>)
            const button = wrapper.find('button')
            expect(button.text()).toEqual('OFF');
            button.onClick();
            expect(button.text()).toEqual('ON');
        });

        it('should be able to switch to OFF if clicked twice', () => {
            const wrapper = shallow(<Toggle/>)
            const button = wrapper.find('button')
            expect(button.text()).toEqual('OFF');
            button.onClick();
            button.onClick();
            expect(button.text()).toEqual('OFF');
        });
    });
  })
```
