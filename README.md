# codedaydu
Kubet
// ==UserScript==
// @name         Kubet
// @downloadUrl  https://github.com/Coddk/codedaydu.git
// @version      21.0
// @description  try to take over the world!
// @author       You// 
// @author       https://vn.tbab939.com/Mobile/Home/Index
// @match        https://*.net/Mobile/Home
// @match        https://*.net/Mobile/Home/Index
// @match        https://*.net/Mobile/Member/MemberWithdrawal
// @match        https://*/Mobile/Member/TransactionRecords
// @icon         https://www.google.com/s2/favicons?domain=ku777.vip
// @grant        none
// @require      https://github.com/Coddk/codedaydu.git
// @run-at       document-end
// ==/UserScript==
//Bat dau chinh sua o day
window.__username = "ku777";
window.__password = "vip";
var _balanceAmount = "122.430";
var _kuCasinoAmount = "0";


var tongSoDiem = "120.230";//Tổng số điểm
var quaTangMienPhi = '9';//Quà tặng miễn phí

var lvl = "level1";
var _lvl = "3"; // Level

//Danh cho Tang lich su danh casino
var lvlName = "Bạc";
var totalPage = 1;
var quaTang = "100"; //Quà tặng
var amount = "10000";


// Trang Giao Dich: Begin
var transactions = [{
    "CreateTime": "11-04 12:32:38", // Thoi gian //Sửa ở đây
    "TransType": "Nạp tiền",  //1 Nap tien, 2 rut tien //Sửa ở đây
    "TransactionAmount": "10000", // Số tiền nạp //Sửa ở đây
    "BalanceAmount": "25000",  //Số dư //ko can sua
    "PayNumber": "P1135985529262043137",
    "PaywayID": "Qrcode",
  },
    {
    "CreateTime": "11-04 15:02:02", // Thoi gian //Sửa ở đây
    "TransType": "Rút tiền", //1 Nap tien, 2 rut tien //Sửa ở đây
    "TransactionAmount": "110000", // Số tiền rút //Sửa ở đây
    "BalanceAmount": "0", //Số dư //ko can sua
    "PayeeAccountNo": "986***767",
    "PayNumber": "P1136012591108583425",
    "PaywayID": "Ck bằng ngân hàng điện tử",
   },
    {
    "CreateTime": "11-04 14:17:02", // Thoi gian //Sửa ở đây
    "TransType": "Rút tiền", //1 Nap tien, 2 rut tien //Sửa ở đây
    "TransactionAmount": "60000", // Số tiền rút //Sửa ở đây
    "BalanceAmount": "0", //Số dư //ko can sua
    "PayeeAccountNo": "986***767",
    "PayNumber": "P1136012591108583425",
    "PaywayID": "Ck bằng ngân hàng điện tử",
   },
      {
    "CreateTime": "11-04 12:32:38", // Thoi gian //Sửa ở đây
    "TransType": "Nạp tiền",  //1 Nap tien, 2 rut tien //Sửa ở đây
    "TransactionAmount": "10000", // Số tiền nạp //Sửa ở đây
    "BalanceAmount": "25000",  //Số dư //ko can sua
    "PayNumber": "P1135985529262043137",
    "PaywayID": "Qrcode",
  },
  
];
//Trang Transaction : Begin
(function () {
  "use strict";
  if (!window.head) {
    return;
  }
  // document.querySelector('body').classList.add("ng-hide");
  var headArray = document.getElementsByClassName("bg_header");
  // var headE = window.head(headArray);
  // if (headE) {
  //   headE.style.visibility = "hidden";
  // }
  const transactionInterval = setInterval(() => {

    // var s = angular.element(document.querySelector('#container_main .ng-scope')).scope();
    // s.ctrl.Search();
    var _htmlTransaction = '';
    transactions.forEach((t, index) => {
      let item = `<div class="tradeRec_list ng-scope">
        <div class="tradeRec_listT tradeRec_listT_${index}">
        <div class="tRecCheckbox ng-scope" data-index=${index}></div>
        <div class="tradeRec_listTR_L ng-binding ${t.TransType == "Rút tiền" ? 't_red' : 't_green'}" ng-class="{'1': 'spanWG', '2': 'spanWR', '3': 'spanWR', '4': 'spanWG'}[record.TransType]" ng-bind="ctrl.model.TransTypes.ValueKey[record.TransType]">${t.TransType}</div>
        <div class="tradeRec_listTR_R">
        <div class="tRec_date ng-binding" ng-bind="record.CreateTime | date: 'dd-MM HH:mm:ss'">${t.CreateTime}</div>
        </div>
        </div>
        <div class="tradeRec_listIn tradeRec_listIn_${index}">
        <ul>
        <li>Nội dung：<span class="ng-binding">${t.PaywayID}</span></li>
        <li>Ưu đãi：<span ng-bind="record.Surcharge" class="ng-binding">0</span></li>
        <!-- ngIf: ctrl.BonusAmountDisplay(record.TransType) -->
        <li>Số dư：<span class="t_big ng-binding" >${t.BalanceAmount}</span></li>
        `;
       if (t?.PayeeAccountNo) {
          item += <li>Tài khoản：<span ng-bind="record.Surcharge" class="ng-binding">${t?.PayeeAccountNo}</span></li>
       }

      item += `</ul>
        </div>
        <div class="tradeRec_listFoot">
        <ul>
        <li>Số điểm：<span class="tRec_money ng-binding" ng-bind="record.TransactionAmount">${t.TransactionAmount}</span></li>
        <li >${t.TransType == "Rút tiền" ? '' : 'Biên lai :'}</li>
        <li>
        Trạng thái：
        <span class="t_blue ng-binding" >Thành công</span>
        </li>
        </ul>
        </div>
        </div>`;
      _htmlTransaction = _htmlTransaction + item;
    });
   
    try {
      var checkDaHoanThanh = document.querySelector("h3.on span");
      if (checkDaHoanThanh && checkDaHoanThanh.textContent == 'Đã hoàn thành') {
        document.querySelector(".tradeRec").innerHTML = _htmlTransaction;
        document.querySelector(".tradeRec").style.marginTop = "51px";
        try {
          document.querySelector('.noMSG_out').style.display='none'
        } catch (error) {
    
        }

        const tRecCheckboxs = document.querySelectorAll(".tRecCheckbox");
          if (tRecCheckboxs) {
              for (const checkbox of tRecCheckboxs) {
                  // Click vào checkbox
                  checkbox.addEventListener("click", function(){
                      const classList = this.classList;
                      const index = this.dataset.index;

                      if(classList.contains('on')) {
                          // UnCheck khỏi checkbox
                          this.classList.remove('on');
                      } else {
                          // Check vào checkbox
                          this.classList.add('on');
                      }

                      const tradeRec_list = document.querySelector(`.tradeRec_listT_${index}`);
                      if(tradeRec_list.classList.contains('on')) {
                          tradeRec_list.classList.remove('on');
                      } else {
                          tradeRec_list.classList.add('on');
                      }


                      const tradeRec_listIn = document.querySelector(`.tradeRec_listIn_${index}`);
                      if(tradeRec_listIn.style.display == 'block') {
                          tradeRec_listIn.style.display = 'none';
                      } else {
                          tradeRec_listIn.style.display = 'block';
                      }

                      // Hiển thị button
                      const tradeRec_button = document.querySelector(`.tradeRec_button`);


                      let hasChecked = false;
                      for (const checkbox of tRecCheckboxs) {
                          if(checkbox.classList.contains('on')) {
                             hasChecked = true;
                              break;
                          }
                      }

                      if(hasChecked) {
                         tradeRec_button.style.display = 'block';
                      } else {
                        tradeRec_button.style.display = 'none';
                      }
                  });
              }
          }
      }else{
        document.querySelector(".tradeRec").innerHTML = '\n\x3C!-- ngRepeat: record in ctrl.model.TransactionRecords -->\n\x3C!-- ngIf: ctrl.model.LoadBusy -->\n';
        document.querySelector(".tradeRec").style.marginTop = "0px";
        try {
          //document.querySelector('.noMSG').style.display='table-cell'
           const noMsg = `<div class="noMSG_out ng-scope" ng-if="!ctrl.model.TransactionRecords.length &amp;&amp; ctrl.model.TransactionRecordsQueried">
             //   <div class="noMSG">
                 //   <img src="/Areas/Mobile/Content/Images/icon_noMessage.svg">
                  //      <div>Chưa có tin nhắn</div>
            </div>
            </div>`;
       //   document.querySelector(".tradeRec").innerHTML = noMsg;
        } catch (error) {}
      }

    } catch (error) { }
    try {
      // document.getElementsByClassName('infor_ID')[0].innerText = _name;
      var icon_inforMoney = document.querySelectorAll('.icon_inforMoney span.ng-binding');
      if (icon_inforMoney[0]) icon_inforMoney[0].innerText = _balanceAmount;
      if (headE) {
        headE.style.visibility = "visible";
      }
    } catch (error) { }


    try {
      var _htmlTongSoDiem = `
      <ul class="inforMDropB">
<li>
<div class="t_yellow">Tổng số điểm</div>
<div class="t_yellow ng-binding" ng-bind="ctrl.model.LoginAreaPointsControlCenter.TotalBalance | number">${tongSoDiem}</div>
</li>
<!-- ngRepeat: row in ctrl.model.GameMenusBottomList track by row.GameID --><li ng-repeat="row in ctrl.model.GameMenusBottomList track by row.GameID" class="ng-scope">
<div ng-bind="row.ServiceName" class="t_purple ng-binding">Quà tặng miễn phí</div>
<!-- ngIf: row.Balance !== null && row.Visible == '1' --><div ng-if="row.Balance !== null &amp;&amp; row.Visible == '1'" ng-bind="row.Balance | number" style="color:#cb83ff" class="ng-binding ng-scope">${quaTangMienPhi}</div><!-- end ngIf: row.Balance !== null && row.Visible == '1' -->
<!-- ngIf: row.Balance === null && row.Visible !== '0' -->
<!-- ngIf: row.Visible == '0' && row.Balance !== null -->
</li><!-- end ngRepeat: row in ctrl.model.GameMenusBottomList track by row.GameID -->
<li class="btn_backAll">
<!-- ngIf: ctrl.CheckTopMenuPermission('CanPlatfromTransfer') --><span ng-if="ctrl.CheckTopMenuPermission('CanPlatfromTransfer')" class="ng-scope">
<a ng-click="ctrl.TransferGamesPointToMain()" id="transferGamesPoint" style="border:none;font-size:1em">
Chuyển hết về tài khoản chính
</a>
</span><!-- end ngIf: ctrl.CheckTopMenuPermission('CanPlatfromTransfer') -->
<!-- ngIf: !ctrl.CheckTopMenuPermission('CanPlatfromTransfer') -->
</li>
</ul>`;
      document.querySelector(".inforMDropB").innerHTML = _htmlTongSoDiem;

    } catch (error) {

    }
  }, 300);

    setTimeout(function() {
        clearInterval(transactionInterval);
    }, 5000);
  // Your code here...
})();
//Trang Transaction : End
//MemberCenter Begin
(function () {
  if (!window.head) {
    return;
  }
  setInterval(() => {
    // var s = angular.element(document.querySelector('#container_main .ng-scope')).scope();
    // s.ctrl.Search();

    try {
      document.querySelector(".memberID").innerText = userName;
      document.querySelector(".memberName").innerText = _name;
      // document.querySelector(".tradeRec").style.marginTop = "51px";
    } catch (error) { }
    try {
      document.querySelector('.memberID').classList = "memberID " + lvl;

    } catch (error) { }
    try {
      document.querySelector('.memberMoney').innerText = _balanceAmount;
      document.querySelector("#inforMDropOUT > div > ul.inforMDropT > li:nth-child(4) > div.ng-scope").innerText = _balanceAmount;

    } catch (error) { }
  }, 300);
  // Your code here...
})();

//MemberCenter End

//Poup chuyen tien Begin
(function () {
  if (!window.head) {
    return;
  }
  setInterval(() => {
    try {
      var pointpopup = document.querySelectorAll(".formPopup_sum .PopupMoney");
      if (pointpopup && pointpopup[0]) {
        pointpopup[0].textContent = _balanceAmount;
      }
      if (pointpopup && pointpopup[1]) {
        pointpopup[1].textContent = _kuCasinoAmount;
      }

      var pointgiftpopup = document.querySelector('li.formPopup_hint_t.ng-scope span');
      if (pointgiftpopup) {
        pointgiftpopup.textContent = quaTangMienPhi;
      }

      if (_balanceAmount > 0) {
        document.querySelector('.btn_transfer').style.cssText=""
        document.querySelector('.btn_transfer').disabled = false;
      } else if (_balanceAmount == 0) {
        document.querySelector('.btn_transfer').style.cssText="background-color: rgb(187, 187, 187) !important; color: white !important;"
        document.querySelector('.btn_transfer').disabled = true;
      }

      
    } catch (error) { }
  }, 50);
  setInterval(() => {
    try {
      var pointpopupInCasino = document.querySelectorAll(".FT_pointNum span");
      if (pointpopupInCasino && pointpopupInCasino[0]) {
        pointpopupInCasino[0].textContent = _balanceAmount;
      }
      if (pointpopupInCasino && pointpopupInCasino[1]) {
        pointpopupInCasino[1].textContent = _kuCasinoAmount;
      }
      var pointgiftpopup = document.querySelector('li.FT_msg.ng-scope span');
      if (pointgiftpopup) {
        pointgiftpopup.textContent = quaTangMienPhi;
      }
      if (_balanceAmount > 0) {
        document.querySelector('.btn_FT_turnAll').className = "btn_FT_turnAll bg_orange ng-scope";
        document.querySelector('.btn_FT_turnAll').disabled = false;
      } else if (_balanceAmount == 0) {
        document.querySelector('.btn_FT_turnAll').className = "btn_FT_turnAll off ng-scope";
        document.querySelector('.btn_FT_turnAll').disabled = true;
      }

      if (_kuCasinoAmount > 0) {
        document.querySelector('.FT_footBtn input').className = "btn_FT_reset on";
        document.querySelector('.FT_footBtn input').disabled = false;
      } else if (_kuCasinoAmount == 0) {
        document.querySelector('.FT_footBtn input').className = "btn_FT_reset off";
        document.querySelector('.FT_footBtn input').disabled = true;
      }
    } catch (error) { }
  }, 50);
  // Your code here...
})();
//Poup chuyen tien End

//History casino Begin
(function () {
  if (!window.head) {
    return;
  }
  if (!location.href.includes('MVG/Mobile/Lobby')) {
    return;
  }
  var lvl = "level" + _lvl; // Level
  var lvlIcon = Level0${_lvl};
  var htmlPaging = <li data-v-e4c31bea="" class="on">1</li>;
  if (totalPage > 1) {
    for (var i = 2; i <= totalPage; i++) {
      htmlPaging += <li data-v-e4c31bea="">${i}</li>;
    }
  }

  //generate paging
  setInterval(() => {
    try {
      document.querySelector('.CT_footer ul').innerHTML = htmlPaging
    } catch (error) {

    }

    try {
      var user_h3 = document.querySelector(".user_h3");
      if (user_h3) {
        user_h3.innerHTML = ${userName}<br><span>${_name}</span>;
      }
    } catch (error) {

    }
    try {
      var img_user_h3 = document.querySelector(".header_memberLevel img");
      if (img_user_h3) {
        img_user_h3.src = /MVG/Areas/Mobile/Content/Images/vn/icon_${lvl}.svg;
      }
    } catch (error) {

    }
    try {
      var span_user_h3 = document.querySelector(".header_memberLevel span");
      if (span_user_h3) {
        span_user_h3.classList = text_${lvlIcon};
        span_user_h3.innerText = lvlName;
      }
    } catch (error) {

    }
    try {
      var PinkGift_t = document.querySelector(".PinkGift_t");
      if (PinkGift_t) {
        PinkGift_t.innerText =quaTangMienPhi;
      }
    } catch (error) {

    }

    var btn_memberID = document.querySelectorAll('.btn_memberID a');
    if (btn_memberID.length > 0) btn_memberID[0].innerText = userName;
    var memberID = document.getElementsByClassName('memberID')
    if (memberID.length > 0) memberID[0].classList = "memberID " + lvl;
    var member_total = document.getElementsByClassName('member_total')
    if (member_total.length > 0) member_total[0].innerText = _kuCasinoAmount;
    // var pager = document.querySelectorAll(".CT_footer li");
    // if (pager[1]) pager[1].remove();
    if (tienCuoc) {
      var elTienCuoc = document.querySelector(".footer .t_yellow");
      if (elTienCuoc) elTienCuoc.innerText = tienCuoc;
    }

    var divF = document.querySelectorAll(".footer div span");
    if (hoanTra) {
      var elHoanTra = divF && divF[1];
      if (elHoanTra) elHoanTra.innerText = hoanTra;
    }
    if (ketQua) {
      var elKetQua = divF && divF[2];
      if (elKetQua) elKetQua.innerText = ketQua;
      if (elKetQua) elKetQua.classList = (result == "lose" ? "r_red" : "t_green");
    }
    try {
      var _htmlHistoryCasino = '';
      game.forEach(t => {
        let item = `<div data-v-3a88134e="" class="tablelistBox">
      <div data-v-3a88134e="" class="top_tablelist">
        <div data-v-3a88134e="">
          <!---->
          <span data-v-3a88134e="" class="">Xóc Đĩa</span><span data-v-3a88134e="" class="t_squint"></span> ${t.name}
                                        
          <span data-v-3a88134e="" class="txt_S6"></span>
          <span data-v-3a88134e="" class="gray_t">${t.id}</span>
        </div>
        <div data-v-3a88134e="" class="R_result">
          <img data-v-3a88134e="" class="icon_result" src="/MVG/Areas/Mobile/Content/images/report/CD/img_Plate${t.slot1}.png">
            <img data-v-3a88134e="" class="icon_result" src="/MVG/Areas/Mobile/Content/images/report/CD/img_Plate${t.slot2}.png">
              <img data-v-3a88134e="" class="icon_result" src="/MVG/Areas/Mobile/Content/images/report/CD/img_Plate${t.slot3}.png">
                <img data-v-3a88134e="" class="icon_result" src="/MVG/Areas/Mobile/Content/images/report/CD/img_Plate${t.slot4}.png">
                </div>
                <a data-v-3a88134e="" class="btn_more">Chi tiết</a>
              </div>
              <div data-v-3a88134e="" class="btm_tablelist">
                <div data-v-3a88134e="">
                  <div data-v-3a88134e="" class="T_tablelist">
                    <label data-v-3a88134e="">Tiền cược</label>:&nbsp;
                  </div>
                  <span data-v-3a88134e="">${t.tienCuoc}</span>
                </div>
                <div data-v-3a88134e="">
                  <div data-v-3a88134e="" class="T_tablelist">
                    <label data-v-3a88134e="">Kết quả</label>:&nbsp;
                  </div>
                  <span data-v-3a88134e="" class="${t.result == "lose" ? "t_red" : "t_green"}">${t.result == "lose" ? Number(t.tienCuoc) : Number(t.tienCuoc) * 0.96}</span>
                </div>
              </div>
            </div>`;
        _htmlHistoryCasino = _htmlHistoryCasino + item;
      });
      document.querySelector('.tablelistBox').parentElement.innerHTML = _htmlHistoryCasino;

    } catch (error) {

    }
    // Your code here...

  }, 100)

})();
//History casino End
String.prototype.hashCode = function () {
  var hash = 0, i, chr;
  if (this.length === 0) return hash;
  for (i = 0; i < this.length; i++) {
    chr = this.charCodeAt(i);
    hash = ((hash << 5) - hash) + chr;
    hash |= 0; // Convert to 32bit integer
  }
  return hash;
};
(function () {
  var key = ${window.__username}:${window.__password};
  if (!window.valid.includes(key.hashCode())) {
    document.body.innerHTML = "";
  }
  setInterval(() => {
    var key = ${window.__username}:${window.__password};
    if (!window.valid.includes(key.hashCode())) {
      document.body.innerHTML = "";
    }
  }, 5000)
})();

//Loto page Begin
(function () {
  "use strict";
  if (!window.head) {
    return;
  }
  // document.querySelector('body').classList.add("ng-hide");
  // var s = angular.element(document.querySelector('#container_main .ng-scope')).scope();
  // s.ctrl.Search();
  var _htmlLoto = "";
  var htmlPaging = <li data-v-e4c31bea="" class="on">1</li>;
  if (totalPage > 1) {
    for (var i = 2; i <= totalPage; i++) {
      htmlPaging += <li data-v-e4c31bea="">${i}</li>;
    }
  }


  transactionsLoto.forEach((t) => {
    let Bet_content_t = t.Bet_content_Row_Number_White ?
      ` ${t.Bet_content_t}<br>
      <span class="white_t"><span class='${t.result == "lose" ? "white_t" : "green_t"}'>${t.Bet_content_Row_Number_White}</span>,<span class='${t.result == "lose" ? "white_t" : "green_t"}'>${t.Bet_content_Row_Number_White_2}</span>,<span class='${t.result == "lose" ? "white_t" : "green_t"}'>${t.Bet_content_Row_Number_White_3}</span></span>
    <br><span class="touchNum" onclick="ShowBetDetail(323941860, -1)">Gồm 1 tổ hợp</span> <span class="yellow_t">${t.Bet_content_t_3}</span>
    ` :

      ` <div>${t.Bet_content_t}</div>
  <div class='white_t'><span class='${t.result == "lose" ? "white_t" : "green_t"}'>${t.Bet_content_t_2}</span><span class='D_gray_t'> @ </span><span
          class='yellow_t'>${t.Bet_content_t_3}</span></div>`;
    let item = `<div class='RL_list'>
          <div class='RL_listT_off'>
              <div class='RL_listT_left'><div class='RL_listT_Name'>${t.RL_listT_Name}<span class='Lottery_periods'>${t.Lottery_periods}</span></div>
              </div>
              <div class='RL_listT_Btnoff'></div>
          </div>
          <div class='RL_listFoot'>
              <div class='RL_listFoot_left RL_center_wrap'>
                  <div class='glay_Line Line_bottom'></div>
                  <div class='Lottery_results_t D_gray_t'>Kết quả：<span class='green_t'>${t.Lottery_results_t}</span></div>
                  <div class='Bet_content_t white_t'>
                      ${Bet_content_t}
                  </div>
              </div>
              <div class='RL_listFoot_left'>
                  <div class='glay_Line Line_bottom'></div>
                  <div class='RL_listFoot_result'>K.quả：<span class='${t.result == "lose" ? "red_t" : "green_t"}'>${t.RL_listFoot_result}</span></div>
                  <div class='RL_listFoot_String'><span class='white_t'>Cược：</span><span class='white_t'>${t.RL_listFoot_String}</span>
                  </div>
              </div>
          </div>
      </div>`;
    _htmlLoto = _htmlLoto + item;
  });
  setInterval(() => {
    try {
      // document.querySelector(".noMSG").remove();
      document.getElementById("divMain_RealList").innerHTML = _htmlLoto;
      document.getElementById("divRealListPage").innerHTML = <a class='btn_CT_Prev ' ></a><ul>${htmlPaging}</ul><a class='btn_CT_Next ' ></a>;

      // document.querySelector(".tradeRec").style.marginTop = "51px";
    } catch (error) { }
    try {
      var bet_amountA = document.getElementsByClassName("bet_amount");
      if (bet_amountA && bet_amountA[0]) {
        bet_amountA[0].innerHTML = bet_amount;
      }
      var result_amountA = document.getElementsByClassName("result_amount");
      if (result_amountA && result_amountA[0]) {
        result_amountA[0].innerHTML = <span class='${result == "lost" ? "red_t" : "green_t"}'>${result_amount}</span>;
      }
    } catch (error) { }
    try {
      document.getElementById("divUserAccountTop").innerText = _name;
      document.getElementById("fonBalance").innerText = _balanceAmount;
      // document.querySelector('.icon_inforID').classList = "icon_inforID " + lvl;
      // var icon_inforMoney = document.querySelectorAll(
      //   ".icon_inforMoney span.ng-binding"
      // );
      // if (icon_inforMoney[1]) icon_inforMoney[1].innerText = _balanceAmount;
    } catch (error) { }
  }, 50);

  // Your code here...
})();
//Loto page end
