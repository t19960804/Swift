# ViewController.swift


import UIKit

class Page1ViewController: UIViewController,UITableViewDelegate,UITableViewDataSource {
    

    @IBAction func nextpage(_ sender: UIButton)
    {
        let obj = acceptUserDataFromPageView[sender.tag]
        self.performSegue(withIdentifier: "要轉場去的StoryBoardId", sender: obj)

        
        
    }
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int
    {
        return acceptUserDataFromPageView.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell
    {
        var cell:CustomCell? = tableView.dequeueReusableCell(withIdentifier: "Cell") as? CustomCell
        if(cell == nil)
        {
            cell = CustomCell(style: UITableViewCellStyle.default, reuseIdentifier: "Cell");
        }
        
       
        cell?.customNameCell.text =
        "\(acceptUserDataFromPageView[indexPath.row].UserName)"
       ========================================
        將cell的按鈕綁定indexPath.row
       ========================================
        cell?.cutomButton.tag = indexPath.row
       ========================================
        將Button的Outlet綁定方法
       ========================================
        cell?.cutomButton.addTarget(self, action: #selector(self.nextpage(_:)), for: .touchUpInside)
        return cell!
    }
    
   
    @IBOutlet weak var UserTableView: UITableView!
    
   
    var acceptUserDataFromPageView = [UserObj]()
    override func viewDidLoad() {
        super.viewDidLoad()
        UserTableView.delegate = self
        UserTableView.dataSource = self

       
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        
    }
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
       ===========================================================
       宣告變數取得ViewController
        let editController = segue.destination as? editController
       ===========================================================
       將sender轉型成與接收資料變數相同型態
        let senderTransForm = sender as? UserObj
       ===========================================================
        editController?.acceptUserDataFromPage1 = senderTransForm!
        

        
    }
    
}
# editController.swift

import UIKit

class editController: UIViewController {
    var backPage1 = Page1ViewController()
    @IBAction func dismiss(_ sender: UIButton){
        
        self.dismiss(animated: true, completion: nil)
        
    }
    @IBOutlet weak var testLabel: UILabel!
    ======================================
    宣告變數接收來自其他ViewController的資料
    var acceptUserDataFromPage1 : UserObj? 
    ======================================
    override func viewDidLoad() {
        super.viewDidLoad()

        testLabel.text = acceptUserDataFromPage1?.UserName
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
       
    }
    

    

}
