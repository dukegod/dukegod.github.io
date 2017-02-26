---
title: react-props
date: 2016-07-03
tags: [JavaScript,React]
---

在es6中使用默认属性props

```
class listTemp extends React.Component {
  constructor(props) {
    super(props);
    //noinspection JSUnresolvedVariable
    this.state = {
      name: this.props.name,
      info: this.props.info,
      image: this.props.image
    }
  }

  componentWillReceiveProps(props) {
    // Do something with props...
    console.log(props);
  }

  render() {
    return (
      <div className='card'>
        <img className='card-img-top' src={this.state.image} />
        <div className='card-block'>
          <h4 className='card-title'>{this.state.name}</h4>
          <p className='card-text'>{this.state.info}</p>
        </div>
      </div>
    );
  }
}

listTemp.defaultProps = {
  name: '默认姓名',
  info: '练习使用react',
  image: '../images/pictuer_brandactivity@2x.png'
};


export default listTemp;

```
