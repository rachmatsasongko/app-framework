<template>
  <div data-page="form-selects" class="page kitchen-sink-ios">
    <div class="navbar">
      <div class="navbar-inner">
        <div class="left sliding"><a class="back link" href="#"><i class="icon icon-back"></i><span>Back</span></a></div>
        <div class="center sliding">Smart Selects</div>
      </div>
    </div>
    <div class="page-content">
      <div class="content-block">Framework7 allows you to easily convert your usual form selects to dynamic pages with radios:</div>
      <div class="list-block">
        <ul>
          <li>
            <a href="#" class="item-link smart-select">
              <select name="fruits">
                  <option value="apple" selected="selected">Apple</option>
                  <option value="pineapple">Pineapple</option>
                  <option value="pear">Pear</option>
                  <option value="orange">Orange</option>
                  <option value="melon">Melon</option>
                  <option value="peach">Peach</option>
                  <option value="banana">Banana</option>
                </select>
              <div class="item-content">
                <div class="item-inner">
                  <div class="item-title">Fruit</div>
                </div>
              </div>
            </a>
          </li>
          <li>
            <a href="#" class="item-link smart-select">
              <select name="car" multiple="multiple">
                  <optgroup label="Japanese">
                    <option value="honda" selected="selected">Honda</option>
                    <option value="lexus">Lexus</option>
                    <option value="mazda">Mazda</option>
                    <option value="nissan">Nissan</option>
                    <option value="toyota">Toyota</option>
                  </optgroup>
                  <optgroup label="German">
                    <option value="audi" selected="selected">Audi</option>
                    <option value="bmw">BMW</option>
                    <option value="mercedes">Mercedes</option>
                    <option value="vw">Volkswagen</option>
                    <option value="volvo">Volvo</option>
                  </optgroup>
                  <optgroup label="American">
                    <option value="cadillac">Cadillac</option>
                    <option value="chrysler">Chrysler</option>
                    <option value="dodge">Dodge</option>
                    <option value="ford" selected="selected">Ford</option>
                  </optgroup>
                </select>
              <div class="item-content">
                <div class="item-inner">
                  <div class="item-title">Car</div>
                </div>
              </div>
            </a>
          </li>
          <li>
            <a href="#" class="item-link smart-select">
              <select name="mac-windows">
                  <option value="mac" selected="selected">Mac</option>
                  <option value="windows">Windows</option>
                </select>
              <div class="item-content">
                <div class="item-inner">
                  <div class="item-title">Mac or Windows</div>
                </div>
              </div>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
