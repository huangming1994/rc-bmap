import React from 'react';
import { Button } from 'antd';
import {
  Map,
  ControlAnchor,
  OverviewMap,
} from 'rc-bmap';
import { getRandomControlAnchor } from 'utils';

class OverviewMapExample extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      offset: {
        width: 0,
        height: 0,
      },
      anchor: ControlAnchor.TOP_RIGHT,
      isOpen: true,
      size: {
        width: 150,
        height: 150,
      },
      events: {
        viewchanged: (event) => {
          console.log('viewchanged', event);
        },
        viewchanging: (event) => {
          console.log('viewchanging', event);
        },
      },
    };
  }

  handleAnchor = () => {
    this.setState({
      anchor: ControlAnchor[getRandomControlAnchor()],
    });
  }

  handleOffset = () => {
    const { offset } = this.state;
    this.setState({
      offset: {
        width: offset.width + 3,
        height: offset.height + 3,
      },
    });
  }

  hideMap = () => {
    const { isOpen } = this.state;
    this.setState({
      isOpen: !isOpen,
    });
  }

  handleSize = () => {
    const { size } = this.state;
    this.setState({
      size: {
        width: size.width + 10,
        height: size.height + 10,
      },
    });
  }

  render() {
    const {
      offset, anchor, size, isOpen, events,
    } = this.state;
    return (
      <React.Fragment>
        <div style={{ height: '90vh' }}>
          <Map
            ak="dbLUj1nQTvDvKXkov5fhnH5HIE88RUEO"
            scrollWheelZoom
          >
            <OverviewMap
              offset={offset}
              anchor={anchor}
              size={size}
              isOpen={isOpen}
              events={events}
            />
          </Map>
          <Button onClick={this.handleOffset}>改变offset</Button>
          <Button onClick={this.handleAnchor}>随机改变停靠位置</Button>
          <Button onClick={this.hideMap}>
            {isOpen ? '收起缩略地图' : '打开缩略地图'}
          </Button>
          <Button onClick={this.handleSize}>改变大小</Button>
        </div>
      </React.Fragment>
    );
  }
}

export default OverviewMapExample;
