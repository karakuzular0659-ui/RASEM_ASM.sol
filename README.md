# RASEM_ASM.sol
RASEM ASM TOKEN 
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

interface IERC20 {
    function totalSupply() external view returns (uint256);
    function balanceOf(address account) external view returns (uint256);
    function transfer(address to, uint256 value) external returns (bool);
    function allowance(address owner, address spender) external view returns (uint256);
    function approve(address spender, uint256 value) external returns (bool);
    function transferFrom(address from, address to, uint256 value) external returns (bool);

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
}

contract RASEMASM is IERC20 {
    address public constant creator = 0x63421296c27720A118e4Fb1B4C0237372ec81b69;
    
    string public constant name = "RASEM ASM";
    string public constant symbol = "RASEM";
    uint8 public constant decimals = 18;
    uint256 public constant override totalSupply = 500000000 * 10**18;

    mapping(address => uint256) public override balanceOf;
    mapping(address => mapping(address => uint256)) public override allowance;

    constructor() {
        balanceOf[creator] = totalSupply;
        emit Transfer(address(0), creator, totalSupply);
    }

    function transfer(address to, uint256 value) public override returns (bool) {
        require(balanceOf[msg.sender] >= value, "Icinde bakiye var");
        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        emit Transfer(msg.sender, to, value);
        return true;
    }

    function approve(address spender, uint256 value) public override returns (bool) {
        allowance[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }

    function transferFrom(address from, address to, uint256 value) public override returns (bool) {
        require(balanceOf[from] >= value, "Icinde bakiye var");
        require(allowance[from][msg.sender] >= value, "Yetki Hatasi");
        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;
        emit Transfer(from, to, value);
        return true;
    }
}
# 🛸 RASEM ASM Token (RASEM)

RASEM ASM, BNB Smart Chain (BSC) ağı üzerinde fütüristik vizyonla geliştirilmiş, topluluk odaklı merkeziyetsiz bir BEP-20 token projesidir.

## 📌 Sözleşme Bilgileri (Contract Details)
* **Token Adı:** RASEM ASM
* **Token Sembolü:** RASEM
* **Ağ (Network):** BNB Smart Chain (BSC)
* **Canlı Kontrat Adresi:** `0xE06f8438E12DCE6328eDD94982c7B0882C5A9Cf7`
* **Toplam Arz (Total Supply):** 500,000,000 RASEM
* **Ondalık Basamak (Decimals):** 18
* **Lisans:** MIT Open Source

## 🛠️ Yazılım Özellikleri
* Tam ERC-20 / BEP-20 Standardı Uyumluluğu
* BscScan ve MetaMask üzerinde %100 Doğrulanmış Sözleşme Yapısı
* Güvenli Harici Yetkilendirme (Approve & TransferFrom Mekanizması)

## 📊 Resmi Bağlantılar
* **BscScan:** https://bscscan.com
